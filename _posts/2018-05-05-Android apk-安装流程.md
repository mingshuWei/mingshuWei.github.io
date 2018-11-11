---
layout:     post
title:      Android apk 安装流程
subtitle:   apk 安装流程简介  
date:       2018-05-05
author:     mingshu
catalog: true
tags:
    - apk 安装
---
# 安装过程
1. 拷贝apk到指定目录，用户安装的apk默认会拷贝到data/app 路径下面，系统预制的apk 在system／ 路径下
2. 解压apk,拷贝文件，创建应用的数据目录。为了加快app的启动，安装时将app的可执行文件dex拷贝大data/dakvik-cache路径下，缓存起来。然后在data/data/目录下创建
应用的数据目录。
3. 解析apk的AndroidManifest.xml Android 系统中有一个记录应用安装卸载的文件，/data/system/packages.xml 每次安装卸载应用都会更新这个文件。
apk 安装过程中，回解析AndroidManifest.xml 文件，解析权限，包名，apk安装位置，版本，userID，签名等。
4. 显示快捷方式，Laucher 从pms中把安装好的应用程序取出来，在桌面上创建快捷方式。

# pms 安装过程
拷贝apk
校验签名
解析app的provider,校验是否与已有的provider冲突
四大组件的解析，注册
dex优化
更新权限信息
安装完成

# 签名
1. MANIFEST.MF
除了三个文件(MANIFEST.MF,CERT.RSA,CERT.SF)，其他的文件都会对文件内容做一次SHA1算法，就是计算出文件的摘要信息,然后用Base64进行编码即可。
如果是一个文件，就用SHA1（或者SHA256）消息摘要算法提取出该文件的摘要然后进行BASE64编码后，作为“SHA1-Digest”属性的值写入到MANIFEST.MF文件中的一个块中。
该块有一个“Name”属性，其值就是该文件在apk包中的路径
2. CERT.SF
 计算这个MANIFEST.MF文件的整体SHA1值，再经过BASE64编码后，记录在CERT.SF主属性块（在文件头上）的“SHA1-Digest-Manifest”属性值值下
 逐条计算MANIFEST.MF文件中每一个块的SHA1，并经过BASE64编码后，记录在CERT.SF中的同名块中，属性的名字是“SHA1-Digest

3. CERT.RSA
这里会把之前生成的 CERT.SF文件， 用私钥计算出签名, 然后将签名以及包含公钥信息的数字证书一同写入  CERT.RSA  中保存。CERT.RSA是一个满足PKCS7格式的文件