## Java Docker 镜像

### 构建Image

使用Dockerfile和默认参数构建java1.7

```
$ docker build -t tonywell/jdk -f alpine-jdk/Dockerfile .
```

打上tag：
```
$ docker tag tonywell/jdk tonywell/jdk:7-alpine
```



使用参数指定jdk版本构建镜像

* JAVA_DISTRIBUTION: jdk or jre (default: jdk)
* JAVA_MAJOR_VERSION：7 or 8 
* JAVA_UPDATE_VERSION: The minor version from any Oracle Java download page.
* JAVA_BUILD_NUMBER: The build number from any Oracle Java download page.
* JDK_TOKEN_DIR：Oracle jdk8 现在下载路径多了一个目录，目录名像是什么MD5

Example:

```
$ docker build -t tonywell/jdk\
  --build-arg JAVA_DISTRIBUTION=jdk \
  --build-arg JAVA_MAJOR_VERSION=8 \
  --build-arg JAVA_UPDATE_VERSION=131 \
  --build-arg JAVA_BUILD_NUMBER=11 \
  --build-arg JDK_TOKEN_DIR=/d54c1d3a095b4ff2b6607d096fa80163
  -f alpine-jdk/Dockerfile .
```

打tag
```
$ docker tag tonywell/jdk tonywell/jdk:8-alpine
```

会构建jdk8u112_b15的镜像
