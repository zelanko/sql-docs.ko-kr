---
title: "SQL Server R Services의 R 상호 운용성 | Microsoft 문서"
ms.custom: 
ms.date: 07/11/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0506b950-34b3-4f11-8e2f-d067a58015bd
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: e393db396c7d41f7eca7851fa10544d697eac5c8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="r-interoperability-in-sql-server"></a>SQL Server의 R 상호 운용성

이 항목 SQL Server 내에서 R에 대 한 실행 하기 위한 메커니즘을 중점적으로 다루며 Microsoft R 및 오픈 소스 오른쪽 간의 차이점을 설명

적용 대상: SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

추가 구성 요소에 대 한 정보를 참조 하십시오. [SQL Server의 새로운 구성 요소](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r.md)합니다.

### <a name="open-source-r-components"></a>오픈 소스 R 구성 요소

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]에는 기본 R 패키지 및 도구의 전체 배포가 포함됩니다. 기본 배포에 포함된 구성 요소에 대한 자세한 내용은 설치하는 동안 기본 위치 `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES\doc\manual`에 설치된 설명서를 참조하세요.

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]를 설치하는 동안 GNU Public License의 조건에 동의해야 합니다. 그 후에 R의 다른 오픈 소스 배포에서 실행하는 것처럼 추가 수정 없이 표준 R 패키지를 실행할 수 있습니다.

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 어떤 방식으로도 R 런타임을 수정하지 않습니다. R 런타임은 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 프로세스 외부에서 실행되며 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]와 독립적으로 실행될 수 있습니다. 하지만 리소스 경합을 피하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 R을 사용하는 동안 이러한 도구를 실행하지 않는 것이 좋습니다.

특정 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스와 연결된 R 기본 패키지 배포는 인스턴스와 연결된 폴더에서 찾을 수 있습니다. 예를 들어 기본 인스턴스에 R 서비스를 설치한 경우 R 라이브러리이 폴더에 있는이 기본적으로:

    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library

마찬가지로, 기본적으로 기본 인스턴스에 연결 된 R 도구 여 폴더에 배치 합니다.

    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin

Microsoft R는 방식과 CRAN에서 발생할 수 있는 R의 기본 배포에 대 한 자세한 내용은 참조 [R 언어 및 Microsoft R 제품 및 기능와의 상호 운용성](https://docs.microsoft.com/en-us/r-server/what-is-r-server-interoperability)

### <a name="additional-r-packages-from-microsoft-r"></a>Microsoft R에서 추가 R 패키지

기본 R 배포 외에도 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 에서는 또한 R의 실행에 원격 계산 컨텍스트는 R의 병렬 실행을 위한 프레임 워크 뿐만 아니라 일부 소유 R 패키지가 포함 되어 있습니다.

R 기본 배포 및 고급 R 기능/패키지의 결합된 R 기능 집합을 **Microsoft R**이라고 합니다. Microsoft R Server(독립 실행형)를 설치할 경우 SQL Server R Services(데이터베이스 내)와 함께 설치되지만 다른 폴더에 있는 똑같은 패키지 집합을 가져옵니다.

Microsoft R에는 더 빠른 수학 처리를 위해 가능할 때마다 사용되는 Intel Math Kernel Library의 배포가 포함됩니다. 예를 들어 기본 선형 대수(BLAS) 라이브러리는 많은 추가 기능 패키지에 사용되고 R 자체에도 사용됩니다. 자세한 내용은 다음 문서를 참조하세요.

+ [How the Intel Math Kernel Speeds up R](http://blog.revolutionanalytics.com/2014/10/revolution-r-open-mkl.html)(Intel Math Kernel을 통해 R 속도를 높이는 방법)
+ [Performance benefits of linking R to multithreaded math libraries](http://blog.revolutionanalytics.com/2010/06/performance-benefits-of-multithreaded-r.html)(R을 다중 스레드 수학 라이브러리에 연결할 경우 성능상 이점)

Microsoft R의 가장 중요한 추가 구성 요소는 **RevoScaleR** 및 **RevoPemaR** 패키지입니다. 이러한 패키지는 성능 향상을 위해 C 또는 C++로 광범위하게 작성된 R 패키지입니다.

+ **RevoScaleR.** 데이터 조작 및 분석을 위한 다양한 API가 포함됩니다. API는 너무 커서 메모리에 맞출 수 없는 데이터 집합을 분석하고 여러 코어 또는 프로세서에 분배되는 계산을 수행하도록 최적화되었습니다.

   RevoScaleR API는 더 큰 확장성을 위해 데이터 하위 집합 사용도 지원합니다. 즉, 대부분의 RevoScaleR 함수는 데이터 청크에서 작동하고 업데이트 알고리즘을 사용하여 결과를 집계할 수 있습니다. 따라서 RevoScaleR 함수를 기반으로 한 R 솔루션은 매우 큰 데이터 집합을 처리할 수 있고 로컬 메모리로 제한되지 않습니다.

  분석에 사용되는 데이터를 더 빠르게 이동하고 저장하기 위해 RevoScaleR 패키지는 .XDF 파일 형식도 지원합니다. XDF 형식은 열 형식 저장소를 사용하고, 이식 가능하고, 텍스트, SPSS 또는 ODBC 연결과 같은 다양한 원본에서 데이터를 로드하고 나서 조작하는 데 사용될 수 있습니다. 

+ **RevoPemaR.** PEMA는 Parallel External Memory Algorithm의 약어입니다. **RevoPemaR** 패키지는 자체 병렬 알고리즘을 개발하는 데 사용할 수 있는 API를 제공합니다. 자세한 내용은 [RevoPemaR Getting Started Guide](https://docs.microsoft.com/r-server/r/how-to-developer-pemar)(RevoPemaR 시작 가이드)를 참조하세요.

시도 하는 것이 좋습니다 [MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package), 분산 처리, 확장성 및 R 코드의 원격 실행을 지 원하는 Microsoft R에서 새 패키지 향상 된 기계 학습 알고리즘을 사용 하 여 Microsoft Research에서 개발 됩니다.

## <a name="next-steps"></a>다음 단계

[아키텍처 개요](../../advanced-analytics/r/architecture-overview-sql-server-r.md)

[R 지원 하도록 SQL Server의 구성 요소](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md)

[보안 개요](../../advanced-analytics/r/security-overview-sql-server-r.md)

