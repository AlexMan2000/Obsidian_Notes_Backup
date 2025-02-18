个人选用Runpod



# 常用操作命令合集
## 拷贝本地文件到服务器
> [!important]
> `scp -P 38599 /path/to/local/file root@connect.yza1.seetacloud.com:/path/to/remote/destination`

> [!important] 使用MobaXTerm工具
> ![](%E8%BF%9C%E7%A8%8BAI%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%A7%9F%E8%B5%81.assets/01fd076bb6b2700e03caefe4e7f65e9b_MD5.jpeg)
> 这里的源文件(夹)路径需要是相对于`D:/Program_Files/SSL_Data`的路径, 需要注意。
> 
> 目标服务器的`/root/`就是连接上之后的根目录



## 在远程主机上开启jupyter服务
> [!important]
> `jupyter lab --ip=0.0.0.0 --port=8888 --no-browser --allow-root --ServerApp.allow_origin='*' --ServerApp.allow_remote_access=True --ServerApp.trust_xheaders=True`


## 为jupyter notebook添加可选Kernel
> [!important]
> `pip install ipykernel`
> 
> `python -m ipykernel install --user --name=myenv --display-name "Python (myenv)"
`