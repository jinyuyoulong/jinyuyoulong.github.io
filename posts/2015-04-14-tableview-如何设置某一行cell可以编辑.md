---
title: tableView 如何设置某一行cell可以编辑
author: fan
type: post
date: 2015-04-14T08:30:39+00:00
url: /tableview-如何设置某一行cell可以编辑/
duoshuo_thread_id:
  - 6278603147225072386
  - 6278603147225072386
categories:
  - iOS

---
当我们使用UITableView的时候，会有这样的情况：我们想要某一条可以编辑删除或不可可以编辑删除，但是tableview默认的是对所有的cell进行设置YES or NO。这时候改怎么办呢，其实我们可以适当使用indexPath
  
&#8211; (BOOL)tableView:(UITableView \*)tableView canEditRowAtIndexPath:(NSIndexPath \*)indexPath
  
{
  
NSIndexPath * indexP =[NSIndexPath indexPathForRow:0 inSection:0];
  
if (indexP == indexPath) {
  
return NO;
  
}
  
return YES;
  
}

<div>
</div>