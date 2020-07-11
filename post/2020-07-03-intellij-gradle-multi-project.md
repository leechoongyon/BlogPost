---
title: Intellij, gradle, multi Project, spring boot 구성 정리
date: 2020-07-03 21:43:00 +/-TTTT
categories: [infra, intellij]
tags: [infra]     # TAG names should always be lowercase
---


> 이 문서는 추후 다시 볼 목적으로 정리한 글입니다.  


## Intellij, gradle, multi Project, spring boot 구성 정리

###### 멀티 프로젝트 구성도
- Root Project : RootProject 
- SubProject : subProject01, subProject02


###### 멀티 프로젝트 구성 방법
1. Intellij 접속 --> Create New Project --> Gradle --> Java(클릭) --> group/artifact 입력 
   - ex) group id : com.test.core, artifactId : TestProject
2. 생성된 것을 기준으로 New --> File --> Module --> Parent RootProject --> 생성
3. RootProject setting.gradle 파일 확인. (SubProject 에는 src, build.gradle 만 있으면 됨.
    ```groovy
    rootProject.name = 'RootProject'  
    include 'SubProject01'  
    include 'SubProject02'
    ```
4. build.gradle 확인
    ```groovy
    plugins {  
        id 'org.springframework.boot' version '2.2.1.RELEASE'  
        id 'java'  
    }  
      
    allprojects {  
      apply plugin: 'java'  
      apply plugin: 'io.spring.dependency-management'  
      apply plugin: 'org.springframework.boot'  
      
      group = 'com.xxx'  
      version = '1.0.0'  
      sourceCompatibility = '1.8'  
      
      configurations {  
            compileOnly {  
                extendsFrom annotationProcessor  
            }  
      }  
      
      repositories {  
              mavenCentral()  
      }  
      
      dependencies {  
            xxx
            ...
      }  
    }  
      
    project(':SubProject01') {  
        bootJar.enabled = false  
        jar.enabled = true  
    }  
      
    project(':SubProject02') {  
        bootJar.enabled = false  
        jar.enabled = true  
        dependencies {
            compile project(':SubProject01')
        }
    }
    ```
