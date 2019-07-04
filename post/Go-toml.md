---
title: "Go Toml"
date: 2019-06-26T15:33:44+08:00
categories:
  - toml
---

[TOC]

常用的配置文件有：ini, ymal, json, toml

说一下为什么要选择 toml。toml 格式是最新公布的配置文件格式，由GitHub创始人 Tom Preston-Werner 发明。TOML 的目标是成为一个极简的配置文件格式。TOML 被设计成可以无歧义地被映射为哈希表，从而被多种语言解析。

### TOML的优势

- 可以添加注释
- 没有缩进要求
- 表达简洁，丰富。
- 大小写敏感

### 写法 config.toml

```toml
[app]
  #app名称
  name = "project-web"
  url = "http://localhost"
  port = ":8080"
  debug = false

[database]
  dirver = "mysql"

[mysql]
  dbname = "@tcp(127.0.0.1:3306)/superstar?charset=utf8"
  username = "root"
  password = "333"

[website]
  static_uri = "/static"
  site_title = "后台管理"
  copy_right = "<small>&copy;2019</small>"

[image]
  image_lib = "Imagick" # GD || Imagick
  image_path   = "../app_images/" #// 目录可读写
  image_url    = "image/" #// http://static.xxx.com/image/car_photo/150x150/19/sdddddd
  image_org    = 'org' #// 原图路径名
  image_tmp    = "tmp" #// 临时路径名
  image_types  = ["jpg","jpeg","png","gif"]
  water_mark   = ""
  #// 汽车品牌LOGO
  [[image.image_categroy]]
    [[image_categroy.car_logo]]
      #// 哈希路径
      paths = "/car_logo/org/"
      #// 支持的尺寸
      sizes = ["100x100","200x200"]
	
```

### 解析

```go
package config

import "github.com/BurntSushi/toml"

type Config struct {
	App struct {
		Name  string
		URL   string
		Port  string
		Debug bool
	}

	Database struct {
		Dirver string
	} `toml:"database"`

	Mysql struct {
		Dbname   string
		Username string
		Password string
	} `toml:"mysql"`

	Website struct {
		static_uri string
		site_title string
		copy_right string
	}

	Image struct {
		ImageLib   string   `toml:"image_lib"`
		ImagePath  string   `toml:"image_path"`
		ImageURL   string   `toml:"image_ur"`
		ImageOrg   string   `toml:"image_org"`
		ImageTmp   string   `toml:"image_tmp"`
		ImageTypes []string `toml:"image_types"`
		WaterMark  string   `toml:"water_mark"`

    ImageCategory struct {

      CarLogo struct {
				Paths string   `toml:"paths"`
				Sizes []string `toml:"sizes"`
			} `toml:"carLogo"`

      ImgLogo struct {
				Paths string `toml:"paths"`
			} `toml:"imgLogo"`
		} `toml:"imageCategory"`
	}
}

// 解析类初始化
var conf *Config

func AppConfig() *Config {
	if conf == nil {
		conf = new(Config)
		file := "../config/config.toml"
		_, err := toml.DecodeFile(file, conf)
		if err != nil {
			fmt.Println("Toml Error!", err.Error())
		}
	}

	return conf
}
```

