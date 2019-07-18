---
title: iOS7之后如何获得APP唯一的身份标识
id: 134
categories:
  - iOS
date: 2015-08-09 11:24:34
tags:
---

**历史：**

1) iOS 5.0以前，iOS 2.0版本以后UIDevice提供一个获取设备唯一标识符的方法uniqueIdentifier，因为该唯一标识符与手机一一对应，苹果觉得可能会泄露用户隐私，所以在 iOS 5.0之后该方法就被废弃掉了。

2）iOS 6.0系统新增了两个用于替换uniqueIdentifier的接口，分别是：identifierForVendor，advertisingIdentifier。

但是APP删除重装后会变化，所以使用WiFi的mac地址来取代已经废弃了的uniqueIdentifier方法。具体的方法晚上有很多，大家感兴趣的可以自己找找，这儿提供一个网址: <http://stackoverflow.com/questions/677530/how-can-i-programmatically-get-the-mac-address-of-an-iphone>

3）iOS 7中苹果再一次无情的封杀mac地址，使用之前的方法获取到的mac地址全部都变成了02:00:00:00:00:00。有问题总的解决啊，于是四处查资料，终于有了思路是否可以使用KeyChain来保存获取到的唯一标示符呢，这样以后即使APP删了再装回来，也可以从KeyChain中读取回来。

**OK 正题来了。。。**

**KeyChain介绍**

 　　我们搞iOS开发，一定都知道OS X里面的KeyChain(钥匙串)，通常要乡镇及调试的话，都得安装证书之类的，这些证书就是保存在KeyChain中，还有我们平时浏览网页记录的账号密码也都是记录在KeyChain中。iOS中的KeyChain相比OS X比较简单，整个系统只有一个KeyChain，每个程序都可以往KeyChain中记录数据，而且只能读取到自己程序记录在KeyChain中的数据。iOS中Security.framework框架提供了四个主要的方法来操作KeyChain:

[![复制代码](http://common.cnblogs.com/images/copycode.gif)]()

```
// 查询
OSStatus SecItemCopyMatching(CFDictionaryRef query, CFTypeRef *result);

// 添加
OSStatus SecItemAdd(CFDictionaryRef attributes, CFTypeRef *result);

// 更新KeyChain中的Item
OSStatus SecItemUpdate(CFDictionaryRef query, CFDictionaryRef attributesToUpdate);

// 删除KeyChain中的Item
OSStatus SecItemDelete(CFDictionaryRef query)
```

[![复制代码](http://common.cnblogs.com/images/copycode.gif)]()

　　这四个方法参数比较复杂，一旦传错就会导致操作KeyChain失败，这块儿文档中介绍的比较详细，大家可以查查官方文档[Keychain Services Reference](https://developer.apple.com/library/ios/documentation/Security/Reference/keychainservices/Reference/reference.html#//apple_ref/doc/uid/TP30000898)。

　　前面提到了每个APP只允许访问自己在KeyChain中记录的数据，那么是不是就没有别的办法访问其他APP存在KeyChain的数据了？

　　苹果提供了一个方法允许同一个发商的多个APP访问各APP之间的途径，即在调SecItemAdd添加数据的时候指定AccessGroup，即访问组。一个APP可以属于同事属于多个分组，添加KeyChain数据访问组需要做一下两件事情:

　　a、在APP target的bulibSetting里面设置Code Signing Entitlements，指向包含AceessGroup的分组信息的plist文件。该文件必须和工程文件在同一个目录下，我在添加访问分组的时候就因为plist文件位置问题，操作KeyChain失败，查找这个问题还花了好久的时间。

![img](http://images.cnitblog.com/blog/302680/201308/30004633-f6d30ed8a07d4e5f909e24a94e0b298e.png)

　　b、在工程目录下新建一个KeychainAccessGroups.plist文件，该文件的结构中最顶层的节点必须是一个名为“keychain-access-groups”的Array，并且该Array中每一项都是一个描述分组的NSString。**对于String的格式也有相应要求，格式为:"AppIdentifier.com.\***"，其中APPIdentifier就是你的开发者帐号对应的ID。**

　　c、在代码中往KeyChain中Add数据的时候，设置kSecAttrAccessGroup，代码如下:

[![复制代码](http://common.cnblogs.com/images/copycode.gif)]()

```
　　 NSString *accessGroup = [NSString stringWithUTF8String:"APPIdentifier.com.cnblogs.smileEvday"];
    if (accessGroup != nil)
    {
#if TARGET_IPHONE_SIMULATOR
        // Ignore the access group if running on the iPhone simulator.
        //
        // Apps that are built for the simulator aren't signed, so there's no keychain access group
        // for the simulator to check. This means that all apps can see all keychain items when run
        // on the simulator.
        //
        // If a SecItem contains an access group attribute, SecItemAdd and SecItemUpdate on the
        // simulator will return -25243 (errSecNoAccessForItem).
#else
        [dictForQuery setObject:accessGroup forKey:(id)kSecAttrAccessGroup];
#endif
    }
```

[![复制代码](http://common.cnblogs.com/images/copycode.gif)]()

　　这段代码是从官方的Demo中直接拷贝过来的，根据注释我们可以看到，模拟器是不支持AccessGroup的，所以才行了预编译宏来选择性添加。

　　**注：appIdentifer就是开发者帐号的那一串标识，如下图所示：**

 　　![img](http://images.cnitblog.com/blog/302680/201310/09212447-ebd65550015647b788d6d6711b0bb90a.png)

　　打开xcode的Organizer，选择Device选项卡，连接设备就可以看到设备上安装的开发者账号描述文件列表，其中第五列最开始的10个字符即为App Identifier，这块儿前面写的不是很清楚，好多朋友加我qq问我，今天特地补上。

 

**三、使用KeyChain保存和获取UDID**

　　

　　说了这么多终于进入正题了，如何在iOS 7上面获取到不变的UDID。我们将第二部分所讲的知识直接应用进来就可以了轻松达到我们要的效果了，下面我们先看看往如何将获取到的identifierForVendor添加到KeyChain中的代码。

[![复制代码](http://common.cnblogs.com/images/copycode.gif)]()

```
+ (BOOL)settUDIDToKeyChain:(NSString*)udid
{
    NSMutableDictionary *dictForAdd = [[NSMutableDictionary alloc] init];
    
    [dictForAdd setValue:(id)kSecClassGenericPassword forKey:(id)kSecClass];
    [dictForAdd setValue:[NSString stringWithUTF8String:kKeychainUDIDItemIdentifier] forKey:kSecAttrDescription];
    
    [dictForAdd setValue:@"UUID" forKey:(id)kSecAttrGeneric];    
    // Default attributes for keychain item.
    [dictForAdd setObject:@"" forKey:(id)kSecAttrAccount];
    [dictForAdd setObject:@"" forKey:(id)kSecAttrLabel];    
    // The keychain access group attribute determines if this item can be shared    // amongst multiple apps whose code signing entitlements contain the same keychain access group.
    NSString *accessGroup = [NSString stringWithUTF8String:kKeyChainUDIDAccessGroup];    if (accessGroup != nil)
    {#if TARGET_IPHONE_SIMULATOR        // Ignore the access group if running on the iPhone simulator.        //
        // Apps that are built for the simulator aren't signed, so there's no keychain access group        // for the simulator to check. This means that all apps can see all keychain items when run        // on the simulator.        //
        // If a SecItem contains an access group attribute, SecItemAdd and SecItemUpdate on the        // simulator will return -25243 (errSecNoAccessForItem).#else
        [dictForAdd setObject:accessGroup forKey:(id)kSecAttrAccessGroup];#endif
    }    const char *udidStr = [udid UTF8String];
    NSData *keyChainItemValue = [NSData dataWithBytes:udidStr length:strlen(udidStr)];
    [dictForAdd setValue:keyChainItemValue forKey:(id)kSecValueData];
    
    OSStatus writeErr = noErr;    if ([SvUDIDTools getUDIDFromKeyChain]) {        // there is item in keychain        [SvUDIDTools updateUDIDInKeyChain:udid];
        [dictForAdd release];        return YES;
    }    else {          // add item to keychain
        writeErr = SecItemAdd((CFDictionaryRef)dictForAdd, NULL);        if (writeErr != errSecSuccess) {
            NSLog(@"Add KeyChain Item Error!!! Error Code:%ld", writeErr);
            
            [dictForAdd release];            return NO;
        }        else {
            NSLog(@"Add KeyChain Item Success!!!");
            [dictForAdd release];            return YES;
        }
    }
    
    [dictForAdd release];    return NO;
}
```

[![复制代码](http://common.cnblogs.com/images/copycode.gif)]()

　　上面代码中，首先构建一个要添加到KeyChain中数据的Dictionary，包含一些基本的KeyChain Item的数据类型，描述，访问分组以及最重要的数据等信息，最后通过调用SecItemAdd方法将我们需要保存的UUID保存到KeyChain中。

　　获取KeyChain中相应数据的代码如下:

[![复制代码](http://common.cnblogs.com/images/copycode.gif)]()

```
+ (NSString*)getUDIDFromKeyChain
{
    NSMutableDictionary *dictForQuery = [[NSMutableDictionary alloc] init];
    [dictForQuery setValue:(id)kSecClassGenericPassword forKey:(id)kSecClass];    
    // set Attr Description for query    [dictForQuery setValue:[NSString stringWithUTF8String:kKeychainUDIDItemIdentifier]
                    forKey:kSecAttrDescription];    
    // set Attr Identity for query
    NSData *keychainItemID = [NSData dataWithBytes:kKeychainUDIDItemIdentifier
                                            length:strlen(kKeychainUDIDItemIdentifier)];
    [dictForQuery setObject:keychainItemID forKey:(id)kSecAttrGeneric];    
    // The keychain access group attribute determines if this item can be shared    // amongst multiple apps whose code signing entitlements contain the same keychain access group.
    NSString *accessGroup = [NSString stringWithUTF8String:kKeyChainUDIDAccessGroup];    if (accessGroup != nil)
    {#if TARGET_IPHONE_SIMULATOR        // Ignore the access group if running on the iPhone simulator.        //
        // Apps that are built for the simulator aren't signed, so there's no keychain access group        // for the simulator to check. This means that all apps can see all keychain items when run        // on the simulator.        //
        // If a SecItem contains an access group attribute, SecItemAdd and SecItemUpdate on the        // simulator will return -25243 (errSecNoAccessForItem).#else
        [dictForQuery setObject:accessGroup forKey:(id)kSecAttrAccessGroup];#endif
    }
    
    [dictForQuery setValue:(id)kCFBooleanTrue forKey:(id)kSecMatchCaseInsensitive];
    [dictForQuery setValue:(id)kSecMatchLimitOne forKey:(id)kSecMatchLimit];
    [dictForQuery setValue:(id)kCFBooleanTrue forKey:(id)kSecReturnData];
    
    OSStatus queryErr   = noErr;
    NSData   *udidValue = nil;
    NSString *udid      = nil;
    queryErr = SecItemCopyMatching((CFDictionaryRef)dictForQuery, (CFTypeRef*)&udidValue);
    
    NSMutableDictionary *dict = nil;
    [dictForQuery setValue:(id)kCFBooleanTrue forKey:(id)kSecReturnAttributes];
    queryErr = SecItemCopyMatching((CFDictionaryRef)dictForQuery, (CFTypeRef*)&dict);    
    if (queryErr == errSecItemNotFound) {
        NSLog(@"KeyChain Item: %@ not found!!!", [NSString stringWithUTF8String:kKeychainUDIDItemIdentifier]);
    }    else if (queryErr != errSecSuccess) {
        NSLog(@"KeyChain Item query Error!!! Error code:%ld", queryErr);
    }    if (queryErr == errSecSuccess) {
        NSLog(@"KeyChain Item: %@", udidValue);        
        if (udidValue) {
            udid = [NSString stringWithUTF8String:udidValue.bytes];
        }
    }
    
    [dictForQuery release];    return udid;
}
```

[![复制代码](http://common.cnblogs.com/images/copycode.gif)]()

　　上面代码的流程也差不多一样，首先创建一个Dictionary，其中设置一下查找条件，然后通过SecItemCopyMatching方法获取到我们之前保存到KeyChain中的数据。

　　

**四、总结**

　　本文介绍了使用KeyChain实现APP删除后依然可以获取到相同的UDID信息的解决方法。

　　你可能有疑问，如果系统升级以后，是否仍然可以获取到之前记录的UDID数据？

　　答案是肯定的，这一点我专门做了测试。就算我们程序删除掉，系统经过升级以后再安装回来，依旧可以获取到与之前一致的UDID。但是当我们把整个系统还原以后是否还能获取到之前记录的UDID，这一点我觉得应该不行，不过手机里面数据太多，没有测试，如果大家有兴趣可以测试一下，验证一下我的猜想。

　　

　　完整代码地址: <https://github.com/smileEvday/SvUDID>

　　大家如果要在真机运行时，需要替换两个地方:

　　第一个地方是plist文件中的accessGroup中的APPIdentifier。

　　第二个地方是SvUDIDTools.m中的kKeyChainUDIDAccessGroup的APPIdentity为你所使用的profile的APPIdentifier。

　　文章和代码中如果有什么不对的地方，欢迎指正，在这儿先谢过了。

文章由[一片枫叶的博客](http://www.cnblogs.com/smileEvday/p/UDID.html#commentform)修改而来