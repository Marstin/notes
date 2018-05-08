## <font color=red text-align=center>linux常用命令</font>
#### 下载
```
  git clone https://github.com/*.git #https协议
  git clone git@github.com:*.git #ssh协议

```
#### 更新
```
  git pull 更新代码
```
#### 强制更新覆盖
```
  git fetch --all
  git reset --hard origin/master
```

#### 加载到缓存区
```
  git add .
```

#### 提交
```
  git push
```

#### 初始化
```
  git init
```

#### 关联到远程库
```
  git remote add origin https://github.com/*
```

#### 合并本地库和远程库
```
  git pull --rebase origin master
```
