---
layout: post
title:  AWS S3 - LifeCycle 관리
description: 비용절감을 목적으로 하는 AWS S3 데이터의 수명주기를 관리
date:   2022-06-08 22:00:00 +0900
image:  '/images/15.jpg'
tags:   [AWS, S3]
---

### AWS - S3 - LifeCycle 관리를 통한 비용절감

클라우드의 최대 장점은 리소스를 유동적으로 조절하여 비용을 관리할 수 있다는 점이다.
데이터 저장소의 역할을 하는 AWS S3는 데이터의 사용 빈도나 크기에 따라 다양한 옵션을 제공한다.
가장 흔히 사용하는 옵션이 Standard이며, 아래에서 설명할 Life Cycle 적용을 통해 자동으로 각 데이터별 관리 정책을 변경할 수 있다.

예시1) AWS Athena 쿼리 결과 Log의 자동 삭제

> 기본적으로 AWS 서비스의 모든 동작은 로그로 기록되는데 특히, 데이터 쿼리 서비스인 Athena의 경우 쿼리의 반환 결과를 로그로 쌓게된다.
이 경우, 사용량이 많은 환경에서는 1~2일만에도 수십 TB의 로그가 발생하게 된다. Standard 옵션에서 1TB의 월 보관비용은 원화로 2~3만원 가량이다.
효용이 없는 로그가 자동으로 쌓임으로서 월 50~100만원의 비용이 추가로 발생할 수 있다는 이야기다. 

** S3 비용 링크 : [[링크]](https://aws.amazon.com/ko/s3/pricing/)

> 위와 같은 로그의 경우, 쿼리의 실행 내역 확인용으로 보관하더라도 며칠 후 삭제가 필요할 것이다.
이 때, 자동으로 특정 기간 후 데이터를 삭제해주는 정책이 LifeCycle을 통해 구현 가능하다.

[[링크]](https://aws.amazon.com/ko/s3/pricing/)의 내용을 살펴보자.

![LifeCycle 적용 순서]({{site.baseurl}}/images/aws_s3_lifecycle_적용방법.png)