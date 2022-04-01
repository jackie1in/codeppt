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
拆装箱、空指针之类的编辑器都会有提示
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
layout: image-left
image: https://api.yimian.xyz/img
equal: false
left: true
---
# ![](https://api.isoyu.com/ARU_GIF_S.php)stream代码块太大
PipelineService.queryPipeline
---
---
# testing
- 回归测试（Regression Testing）
>回归测试是指修改了旧代码后，重新进行测试以确认修改没有引入新的错误或导致其他代码产生错误。自动回归测试将大幅降低系统测试、维护升级等阶段的成本。回归测试作为软件生命周期的一个组成部分，在整个软件测试过程中占有很大的工作量比重，软件开发的各个阶段都会进行多次回归测试。在渐进和快速迭代开发中，新版本的连续发布使回归测试进行的更加频繁，而在极端编程方法中，更是要求每天都进行若干次回归测试。因此，通过选择正确的回归测试策略来改进回归测试的效率和有效性是非常有意义的。
- 冒烟测试（smoke testing)
>冒烟测试在测试中发现问题，找到了一个Bug，然后开发人员会来修复这个Bug。这时想知道这次修复是否真的解决了程序的Bug，或者是否会对其它模块造成影响，就需要针对此问题进行专门测试，这个过程就被称为SmokeTest。在很多情况下，做SmokeTest是开发人员在试图解决一个问题的时候，造成了其它功能模块一系列的连锁反应，原因可能是只集中考虑了一开始的那个问题，而忽略其它的问题，这就可能引起了新的Bug。SmokeTest优点是节省测试时间，防止build失败。缺点是覆盖率还是比较低。

回归测试关注是代码本身是否能编译通过、旧有的逻辑未变是否能够正常回归（优化、添加新功能分支等）<br>冒烟测试针对bug，是否对其他功能模块影响，只能测试一个主要逻辑无法覆盖到所有逻辑
---
layout: center-image
image: https://api.ixiaowai.cn/api/api.php
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