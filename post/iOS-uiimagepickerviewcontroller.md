---
title: 简单实用UIImagePickerViewController
tags:
  - UI
  - UIImagePickerViewController
id: 349
categories:
  - iOS
date: 2016-03-09 13:31:36
---

创建createVC

        UIImagePickerController* ipc = [[UIImagePickerController alloc] init];
        ipc.sourceType = UIImagePickerControllerSourceTypePhotoLibrary; //图像来源
        ipc.delegate = self;
        [self presentModalViewController:ipc animated:YES];
            ````
            完善代理delegate方法
            ````
            //选择图片
    //- (void)imagePickerController:(UIImagePickerController *)picker didFinishPickingImage:(UIImage *)image editingInfo:(NSDictionary *)editingInfo
    - (void)imagePickerController:(UIImagePickerController *)picker didFinishPickingMediaWithInfo:(NSDictionary *)info{
        headView.image = [info objectForKey:@"UIImagePickerControllerOriginalImage"];
        [picker dismissModalViewControllerAnimated:YES];
    }

    //取消
    - (void)imagePickerControllerDidCancel:(UIImagePickerController *)picker{
        [picker dismissModalViewControllerAnimated:YES];
    }
    