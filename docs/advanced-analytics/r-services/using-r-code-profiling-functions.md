---
title: "프로 파일링 함수 R 코드를 사용 하 여 | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 132db249-b9f1-48f5-a63e-c9806cacc4af
caps.latest.revision: 6
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# 프로 파일링 함수 R 코드를 사용 하 여
R 스크립트 실행을 모니터링 하는 SQL Server 리소스와 도구를 사용 하는 것 외에도 내부 함수 호출에 대 한 자세한 정보를 보려면 다른 R 패키지에서 제공 하는 성능 도구를 사용할 수 있습니다. 이 항목에서는 시작 하기 위한 몇 가지 기본적인 리소스의 목록을 제공 합니다. 전문가 안내에 대 한 것이 좋습니다 장에 [성능](http://adv-r.had.co.nz/Performance.html) "" 고급 R "", Hadley Wickham 하 여 책에 있습니다.

## <a name="using-rprof"></a>RPROF를 사용 하 여

*rprof* 기본 패키지에 포함 하는 함수 **유틸리티**, 는 기본적으로 로드 됩니다. 한 가지 이점은 *rprof* 따라서 모니터링에서 성능 부하를 절감 샘플링을 수행 하 되는 것은 합니다.

R 코드에서 프로 파일링을 사용 하려면이 함수를 호출 하 고 쓸 로그 파일의 위치 이름을 포함 하 여 해당 매개 변수를 지정 합니다. 에 대 한 도움말을 참조 하십시오 *rprof* 대 한 자세한 내용은 합니다.

일반적으로 *rprof* 함수의 호출 스택을 파일에 지정 된 간격으로 작성 하 여 작동 합니다. 사용할 수는 *summaryRprof* 출력 파일을 처리 하는 함수입니다. 

프로 파일링 수 설정 및 해제 코드에서. 에 대 한 호출의 시퀀스 프로 파일링을 설정 하 고 프로 파일링을 일시 중단 다시, 하려면 사용 *rprof*:

1. 프로 파일링 출력 파일을 지정 합니다.

    ```R
    varOutputFile <- "C:/TEMP/run001.log")
    Rprof(varOutputFile)
    ```
2. 프로 파일링 해제
    ```R
    Rprof(NULL)
    ```
    
3. 프로 파일링 다시 시작
    ```R
    Rprof(append=TRUE)
    ```


> [!NOTE] 이 함수를 사용 하 여 Windows Perl 코드를 실행 하는 컴퓨터에 설치할 수 있도록 해야 합니다. 따라서 R 환경에서 개발 하는 동안 코드를 프로 파일링 한 다음 SQL server 디버깅 된 코드를 배포 하는 것이 좋습니다.  


## <a name="r-system-functions"></a>시스템 함수 R

R 언어는 시스템 변수 내용을 반환 하기 위한 많은 기본 패키지 함수를 포함 합니다. 

예를 들어 R 코드의 일부로 사용할 수 있습니다 `Sys.timezone` 현재 표준 시간대를 가져오려는 또는 `Sys.Time` R.에서 시스템 시간을 가져올 수 

개별 R 시스템 함수에 대 한 정보를 가져오려면 R에 대 한 인수로 함수 이름을 입력 `help()` 함수 R 명령 프롬프트에서.

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>R에서 프로 파일링 및 디버깅

Microsoft R Open, 기본적으로 설치에 대 한 설명서에는 수동 프로 파일링 및 디버깅을 자세히 설명 하는 R 언어에 대 한 확장을 개발에 포함 되어 있습니다.

장 역시 사용할 수 있는 온라인: [https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)

### <a name="location-of-r-help-files"></a>R 도움말 파일의 위치

C:\Program Files\Microsoft SQL Server\MSSQL13 합니다. MSSQLSERVER\R_SERVICES\doc\manual


