---
title: R 코드 프로파일링 함수 사용 | Microsoft 문서
ms.custom: ''
ms.date: 11/29/2016
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 13ee1c64cf5caf9618fd8515aa467706eed331fe
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="using-r-code-profiling-functions"></a>R 코드 프로파일링 함수 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 리소스 및 도구를 사용하여 R 스크립트 실행을 모니터링할 뿐 아니라 다른 R 패키지에서 제공된 성능 도구를 사용하여 내부 함수 호출에 대한 추가 정보를 가져올 수 있습니다. 이 항목에서는 시작하기 위한 몇 가지 기본 리소스 목록을 제공합니다. 전문가인 경우에는 Hadley Wickham의 서적 ""Advanced R""에서 [Performance](http://adv-r.had.co.nz/Performance.html) 장을 참조하는 것이 좋습니다.

## <a name="using-rprof"></a>RPROF 사용

*rprof*는 기본적으로 로드되는 기본 패키지 **utils**에 포함된 함수입니다. *rprof*의 한 가지 장점은 샘플링을 수행하므로 모니터링에 대한 성능 부하가 감소한다는 것입니다.

코드에서 R 프로파일링을 사용하려면 이 함수를 호출하고 해당 매개 변수(예: 기록될 로그 파일의 위치 이름)를 지정합니다. 자세한 내용은 *rprof*에 대한 도움말을 참조하세요.

일반적으로 *rprof* 함수는 지정된 간격으로 호출 스택을 파일에 쓰는 방식으로 실행됩니다. *summaryRprof* 함수를 사용하여 출력 파일을 처리할 수 있습니다. 

코드에서 프로파일링 기능을 켜고 끌 수 있습니다. 프로파일링을 켜고 프로파일링을 일시 중지했다 다시 시작하려면 *rprof*에 대한 호출 시퀀스를 사용합니다.

1. 프로파일링 출력 파일을 지정합니다.

    ```R
    varOutputFile <- "C:/TEMP/run001.log")
    Rprof(varOutputFile)
    ```
2. 프로파일링 끄기
    ```R
    Rprof(NULL)
    ```
    
3. 프로파일링 다시 시작
    ```R
    Rprof(append=TRUE)
    ```


> [!NOTE]
> 이 함수를 사용하려면 코드가 실행되는 컴퓨터에 Windows Perl이 설치되어 있어야 합니다. 따라서 R 환경에서 개발하는 동안 코드를 프로파일링하고 디버그된 코드를 SQL Server에 배포하는 것이 좋습니다.  


## <a name="r-system-functions"></a>R 시스템 함수

R 언어에는 시스템 변수의 내용을 반환하기 위한 다양한 기본 패키지 함수가 포함됩니다. 

예를 들어 R 코드의 일부로 `Sys.timezone`을 사용하여 현재 표준 시간대를 가져오거나 `Sys.Time`을 사용하여 R에서 시스템 시간을 가져올 수 있습니다. 

개별 R 시스템 함수에 대한 정보를 확인하려면 R 명령 프롬프트에서 함수 이름을 `help()` 함수의 인수로 입력합니다.

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>R에서 디버그 및 프로파일링

기본적으로 설치되는 Microsoft R Open에 대한 설명서에는 프로파일링 및 디버그를 자세히 설명하는 R 언어에 대한 확장 개발 매뉴얼이 포함됩니다.

장은 온라인도 사용할 수 있습니다: [https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)

### <a name="location-of-r-help-files"></a>R 도움말 파일 위치

C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\doc\manual



