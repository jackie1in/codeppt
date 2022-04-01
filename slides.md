---
theme: light-icons
layout: intro
image: https://tuapi.eees.cc/api.php?category=dongman&type=302
themeConfig:
  primary: '#4d7534'
lineNumbers: true
drawings:
  persist: false
info: |
  ## 一些演示文档
  我的第一个 [Slidev](http://sli.dev/) 演示!
title: 'gradle java以及一些代码规范的例子'  
---

  <div class="mb-4 absolute bottom-4 left-12">
    <span class="text-6xl text-primary-lighter text-opacity-80" style="font-weight:500;" >
      帅哥 <light-icon icon="man"/>
    </span>
    <div class="text-9xl text-white text-opacity-60" style="font-weight:600;" >
      林海
    </div> 
  </div>****

---
layout: dynamic-image
image: https://www.dmoe.cc/random.php
equal: false
left: true
---

# 主要内容

- [**.env的使用**](./3)
- **使用插件加快导入项目**
- **不规范代码**
- **@validate参数验证**
- **swagger根据group渲染的**
- **unit test with testcontainer**

---
layout: dynamic-image
image: https://www.dmoe.cc/random.php
equal: false
left: true
---

# .env的使用
```bash {10|all}
#!/usr/bin/env
SPRING_CLOUD_CONFIG_PROFILE=ci
SPRING_CLOUD_CONFIG_DISCOVERY_ENABLED=false
SEATA_SERVICE_GROUPLIST_DEFAULT=172.20.23.219:8091
SEATA_ENABLED=false
SPRING_CLOUD_CONFIG_URI=http://172.20.23.219:9000
SPRING_RABBITMQ_ADDRESSES=172.20.23.219:5672
JENKINS_CHECKURL=http://172.20.23.219:444
EUREKA_CLIENT_SERVICEURL_DEFAULTZONE=http://172.20.23.219:9001/eureka/
DOCKER_HOST=tcp://172.20.23.219:2375
TESTCONTAINERS_REUSE_ENABLE=true
```

### [idea安装插件](https://github.com/ashald/EnvFile)

### vscode
```json {6|all}
{
    "java.format.settings.url": "checkstyle/eclipse-codestyle.xml",
    "java.format.settings.profile": "P3C-CodeStyle",
    "java.test.config":{
        "name": "loca test, need start docker compose",
        "envFile": "${workspaceFolder}/.env"
    }
}
```

---
layout: dynamic-image
image: https://acg.toubiec.cn/random.php
equal: false
left: true
---

# 使用插件加快导入项目
## idea
```bash
cd ~/yinhai/my-devops
rm -rf .idea
./gradlew cleanIdea idea
idea .
``` 
## eclipse/vscode
```bash
cd ~/yinhai/my-devops
./gradlew cleanEclipse eclipse
code .
``` 

---
layout: dynamic-image
image: https://api.ixiaowai.cn/mcapi/mcapi.php
equal: false
left: true
---

# 不规范代码
编辑器都会有提示，看到了一定要加上相关代码
### auto unboxing
```java
@Test
public void unboxing_test() {
    Integer a = null;
    int b = 1;
    Assertions.assertThrows(NullPointerException.class, () -> {
        System.out.println("auto unboxing null pointer reproduce");
        if (a == b){
            
        }
    });
}
```
### auto boxing
```java
@Test
public void boxing_test() {
    Long a = 128L;
    int b = 128;
    assertThat(a.equals(b)).isFalse();
    assertThat(Objects.equals(a, b)).isFalse();
}
```
---
layout: dynamic-image
image: https://api.yimian.xyz/img
equal: false
left: true
---
# ![](https://api.isoyu.com/ARU_GIF_S.php)stream代码块太大

PipelineService.queryPipeline

---
layout: center-image
image: https://api.ixiaowai.cn/api/api.php
equal: false
left: true
---
# @validate参数验证
---
layout: center-image
image: https://api.paugram.com/wallpaper/
---
# swagger根据group渲染的
---
layout: dynamic-image
image: https://img.paulzzh.tech/touhou/random
---
# unit test with testcontainer

### junit5 fluent api
```java
assertThat(Objects.equals(a, b)).isFalse();
```
### 如何使用testcontainer
```java
@DevopsTest
public class UserCenterApplicationTest implements IPostgresContainer {
}
```
```java
@DBIntegrationTest
public class ProjectGroupPermissionServiceImplTest implements IPostgresContainer {
  // 需要去mock我们的service设置模拟数据，如果不想去模拟本地service可以使用@DevopsTest
}
```
### 配合env实现单元测试
```groovy {3|all}
test {
    if(env.isPresent("DOCKER_HOST")){
        environment(env.allVariables)
    }
    useJUnitPlatform()
}
```