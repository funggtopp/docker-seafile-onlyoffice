# docker-seafile-onlyoffice
*** docker-compose 一键配置 seafile+onlyoffice ***
## 启动 seafile 和 onlyoffice
### 克隆本站至docker-seafile-onlyoffice目录，目录下运行
```
docker-compose up -d
```

等到几分钟后，访问该机器ip的80端口可以打开seafile，访问该机器的8080端口显示Document Server is running
### 集成 seafile 和 onlyoffice

等待seafile正常启动后，进入容器修改配置文件
```
docker exec -it seafile bash
vim conf/seahub_settings.py
```

在最下面追加如下内容
```
ENABLE_ONLYOFFICE = True
VERIFY_ONLYOFFICE_CERTIFICATE = False
ONLYOFFICE_APIJS_URL = 'http://10.110.25.201:8080/web-apps/apps/api/documents/api.js' #ip 改为 本机ip
ONLYOFFICE_FILE_EXTENSION = ('doc', 'docx', 'ppt', 'pptx', 'xls', 'xlsx', 'odt', 'fodt', 'odp', 'fodp', 'ods', 'fods')
ONLYOFFICE_EDIT_FILE_EXTENSION = ('docx', 'pptx', 'xlsx')
```

退出容器后重启该容器
```
exit
docker restart seafile
```

稍等片刻后登陆 seafile 查看私人资料库下的 seafile-tutorial.doc 是否能在线编辑。
### 配置 seaflie

用admin账户登录后，点击右上角头像->系统管理->设置。<br>
将URL的SERVICE_URL和FILE_SERVER_ROOT改为http://<机器ip>和http://<机器ip>/seafhttp。


## 特别鸣谢
链接：https://www.jianshu.com/p/45ac766b057e
