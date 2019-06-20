---
title: R 코드 프로 파일링 함수-SQL Server Machine Learning Services를 사용 합니다.
description: 성능을 향상 시키고 내부 함수 호출에 대 한 정보를 반환할 R 함수를 프로 파일링을 사용 하 여 SQL Server에 R 계산에 더 빠른 결과 가져옵니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c9195a6c2b9a2192e9d8fd04ce3e5d2592b1b23e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642254"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>성능 향상을 위해 R 코드 프로 파일링 함수 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 리소스 및 도구를 사용하여 R 스크립트 실행을 모니터링할 뿐 아니라 다른 R 패키지에서 제공된 성능 도구를 사용하여 내부 함수 호출에 대한 추가 정보를 가져올 수 있습니다. 

> [!TIP]
> 이 문서에서는 시작 하기 위한 기본 리소스를 제공 합니다. 전문가 지침에 대 한 것이 좋습니다 합니다 *성능* 단원의 [Hadley wickham "Advanced R"](http://adv-r.had.co.nz)합니다.

## <a name="using-rprof"></a>RPROF 사용

[*rprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) 는 기본 패키지에 포함 된 함수 [ **utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1)는 기본적으로 로드 됩니다. 

일반적으로 *rprof* 함수는 지정된 간격으로 호출 스택을 파일에 쓰는 방식으로 실행됩니다. 사용할 수는 [ *summaryRprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) 출력 파일을 처리 하는 함수입니다. *rprof*의 한 가지 장점은 샘플링을 수행하므로 모니터링에 대한 성능 부하가 감소한다는 것입니다.

코드에서 R 프로파일링을 사용하려면 이 함수를 호출하고 해당 매개 변수(예: 기록될 로그 파일의 위치 이름)를 지정합니다. 코드에서 프로파일링 기능을 켜고 끌 수 있습니다. 다음 구문을 기본 사용법을 보여 줍니다. 

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

Microsoft R Open을 기본적으로 설치 된 설명서에 설명 하는 R 언어에 대 한 확장 개발 매뉴얼이 포함 됩니다 [프로 파일링 및 디버깅](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging) 자세히 설명에서 합니다. C:\Program Files\Microsoft SQL Server\MSSQL13 시 컴퓨터에 동일한 설명서를 찾을 수 있습니다. MSSQLSERVER\R_SERVICES\doc\manual 합니다.

## <a name="see-also"></a>참고자료

+ [R 유틸리티 패키지](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ ["고급 R" Hadley wickham](http://adv-r.had.co.nz)
