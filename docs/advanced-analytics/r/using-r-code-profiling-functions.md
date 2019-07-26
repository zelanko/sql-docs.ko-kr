---
title: R 코드 프로파일링 함수 사용
description: R 프로 파일링 함수를 사용 하 여 내부 함수 호출에 대 한 정보를 반환 함으로써 SQL Server에서 R 계산에 대 한 성능 향상 및 더 빠른 결과를 얻습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a586a4f7656dd0319e3139e05ba1bea6c8d96abe
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469842"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>R 코드 프로 파일링 함수를 사용 하 여 성능 향상
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 리소스 및 도구를 사용하여 R 스크립트 실행을 모니터링할 뿐 아니라 다른 R 패키지에서 제공된 성능 도구를 사용하여 내부 함수 호출에 대한 추가 정보를 가져올 수 있습니다. 

> [!TIP]
> 이 문서에서는 시작 하는 데 도움이 되는 기본 리소스를 제공 합니다. 전문가 지침을 보려면 [Hadley Wickham에서 "Advanced R"](http://adv-r.had.co.nz)의 *성능* 섹션을 권장 합니다.

## <a name="using-rprof"></a>RPROF 사용

[*rprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) 는 기본적으로 로드 되는 기본 패키지 [**유틸리티**](https://www.rdocumentation.org/packages/utils/versions/3.5.1)에 포함 된 함수입니다. 

일반적으로 *rprof* 함수는 지정된 간격으로 호출 스택을 파일에 쓰는 방식으로 실행됩니다. 그런 다음 [*summaryRprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) 함수를 사용 하 여 출력 파일을 처리할 수 있습니다. *rprof*의 한 가지 장점은 샘플링을 수행하므로 모니터링에 대한 성능 부하가 감소한다는 것입니다.

코드에서 R 프로파일링을 사용하려면 이 함수를 호출하고 해당 매개 변수(예: 기록될 로그 파일의 위치 이름)를 지정합니다. 코드에서 프로파일링 기능을 켜고 끌 수 있습니다. 다음 구문에서는 기본 사용법을 보여 줍니다. 

```R
# Specify profiling output file.
varOutputFile <- "C:/TEMP/run001.log")
Rprof(varOutputFile)

# Turn off profiling
Rprof(NULL)
    
# Restart profiling
Rprof(append=TRUE)
```

> [!NOTE]
> 이 함수를 사용하려면 코드가 실행되는 컴퓨터에 Windows Perl이 설치되어 있어야 합니다. 따라서 R 환경에서 개발하는 동안 코드를 프로파일링하고 디버그된 코드를 SQL Server에 배포하는 것이 좋습니다.  


## <a name="r-system-functions"></a>R 시스템 함수

R 언어에는 시스템 변수의 내용을 반환하기 위한 다양한 기본 패키지 함수가 포함됩니다. 예를 들어 R 코드의 일부로 `Sys.timezone`을 사용하여 현재 표준 시간대를 가져오거나 `Sys.Time`을 사용하여 R에서 시스템 시간을 가져올 수 있습니다. 

개별 R 시스템 함수에 대한 정보를 확인하려면 R 명령 프롬프트에서 함수 이름을 `help()` 함수의 인수로 입력합니다.

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>R에서 디버그 및 프로파일링

기본적으로 설치 되는 Microsoft R Open 설명서에는 [프로 파일링 및 디버깅](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging) 에 대해 자세히 설명 하는 R 언어 확장을 개발 하는 데 대 한 설명서가 포함 되어 있습니다. 컴퓨터에서 C:\Program Files\Microsoft SQL Server\MSSQL13. 같은 문서를 찾을 수 있습니다. MSSQLSERVER\R_SERVICES\doc\manual.

## <a name="see-also"></a>참조

+ [유틸리티 R 패키지](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ [Hadley Wickham의 "고급 R"](http://adv-r.had.co.nz)
