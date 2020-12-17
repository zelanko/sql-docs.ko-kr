---
title: R 코드 프로파일링 함수를 사용하여 성능 향상
description: R 프로파일링 기능을 사용하여 SQL Server에서 R 계산에 대한 성능을 향상하고 더 빠른 결과를 얻을 수 있는 유용한 정보를 수집합니다. *rprof* 함수는 내부 함수 호출에 대한 정보를 수집하고 반환합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/30/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 53c3e7f55fa21d033bfda3f2e660bd1b9a92991f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470744"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>R 코드 프로파일링 함수를 사용하여 성능 향상
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이 문서에서는 내부 함수 호출에 대한 정보를 가져오기 위해 R 패키지가 제공하는 성능 도구를 설명합니다. 이 정보를 사용하여 코드의 성능을 향상시킬 수 있습니다.

> [!TIP]
> 이 문서에서는 시작하는 데 도움이 되는 기본 리소스를 제공합니다. 전문가인 경우에는 [Hadley Wickham의 서적 ""Advanced R""](http://adv-r.had.co.nz)에서 *Performance* 섹션을 참조하는 것이 좋습니다.

## <a name="using-rprof"></a>RPROF 사용

[*rprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof)는 기본적으로 로드되는 기본 패키지 [**utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1)에 포함된 함수입니다. 

일반적으로 *rprof* 함수는 지정된 간격으로 호출 스택을 파일에 쓰는 방식으로 실행됩니다. [*summaryRprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) 함수를 사용하여 출력 파일을 처리할 수 있습니다. *rprof* 의 한 가지 장점은 샘플링을 수행하므로 모니터링에 대한 성능 부하가 감소한다는 것입니다.

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

기본적으로 설치되는 Microsoft R Open에 대한 설명서에는 [프로파일링 및 디버깅](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)을 자세히 설명하는 R 언어에 대한 확장 개발 매뉴얼이 포함됩니다.

## <a name="next-steps"></a>다음 단계

+ SQL Server에서의 R 스크립트 최적화에 대한 자세한 내용은 [R 성능 조정 및 데이터 최적화](r-and-data-optimization-r-services.md)를 참조하세요.
+ SQL Server에서의 성능 조정에 대한 자세한 내용은 [SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 성능 센터](/sql/relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database)를 참조하세요.
+ utils 패키지에 대한 자세한 내용은 [R Utils Package](https://www.rdocumentation.org/packages/utils/versions/3.5.1)를 참조하세요.
+ R 프로그래밍에 대한 자세한 설명은 [Hadley Wickham의 서적 "Advanced R"](http://adv-r.had.co.nz)을 참조하세요.
