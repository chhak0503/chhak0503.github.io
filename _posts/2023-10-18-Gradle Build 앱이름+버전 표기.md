---
title: Gradle Build 앱이름+버전 표기
author: chhak
date: 2023-10-18 00:00:00 +0800
categories: [Spring]
tags: [Spring, Gradle]
---

#### Java 코드

```
@Autowired
private BuildProperties buildProperties; // 빌드 정보 인스턴스 주입

@GetMapping("/index")
public String index(Model model){

    // build.gradle 파일 맨 밑에 빌드 정보를 가져오기 위해 buildInfo() 호출 해야됨
    String appName = buildProperties.getName(); // settings.gradle 파일에서 앱이름 가져옴
    String version = buildProperties.getVersion(); // build.gradle 파일에서 버전값 가져옴

    System.out.println("appName : " + appName);
    System.out.println("version : " + version);

	model.addAttribute("appInfo", appName+version);

	return "/index";
}
```

#### build.gradle 코드

```
...
dependencies {...}

// Java에서 빌드정보 참조를 위해 gradle buildInfo() 실행
springBoot {
    buildInfo()
}

tasks.named('test') {
    useJUnitPlatform()
}
```
