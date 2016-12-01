## Java Docker 镜像

### 构建Image

使用Dockerfile和默认参数构建java1.7

```
$ docker build -t tonywell/alpine-jdk7 -f alpine-jdk/Dockerfile .
```



使用参数指定jdk版本构建镜像

* JAVA_DISTRIBUTION: jdk or jre (default: jdk)
* JAVA_MAJOR_VERSION：7 or 8 
* JAVA_UPDATE_VERSION: The minor version from any Oracle Java download page.
* JAVA_BUILD_NUMBER: The build number from any Oracle Java download page.

Example:

```
$ docker build -t tonywell/jdk{minor version} \
  --build-arg JAVA_DISTRIBUTION=jdk \
  --build-arg JAVA_MAJOR_VERSION=8 \
  --build-arg JAVA_UPDATE_VERSION=112 \
  --build-arg JAVA_BUILD_NUMBER=15 \
  -f alpine-jdk/Dockerfile .
```

会构建jdk8u112_b15的镜像