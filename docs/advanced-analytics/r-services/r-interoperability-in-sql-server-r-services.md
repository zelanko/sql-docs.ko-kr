---
title: "SQL Server R 서비스의 R 상호 운용성 | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0506b950-34b3-4f11-8e2f-d067a58015bd
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# SQL Server R 서비스의 R 상호 운용성

내에서 R에 대 한 실행에 대 한 메커니즘에 중점적 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], Microsoft R 및 오픈 소스 R. 사이의 차이점을 설명 하 고 추가 구성 요소에 대 한 정보를 참조 하십시오. [SQL Server의 새로운 구성 요소](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)합니다.

### 오픈 소스 R 구성 요소

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 전체 배포 기본 R 패키지 및 도구에 포함 되어 있습니다. 기본 배포에 포함 된 항목에 대 한 자세한 내용은 다음 기본 위치에 설치 하는 동안 설치 설명서를 참조 합니다.
`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES\doc\manual`

설치 과정의 일부로 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], GNU 공용 사용권 약관에 동의 해야 합니다. 그리고 나면 R.의 다른 오픈 소스 분포에서와 마찬가지로 표준 R 패키지를 더 이상의 수정 없이 실행할 수 있습니다.

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 어떤 방식으로든에서 R 런타임을 수정 하지 않습니다. R 런타임 외부에서 실행 되는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 처리 하 고의 독립적으로 실행할 수 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 그러나 권장 하는 동안 이러한 도구를 실행 하지 않으면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] R을 사용 하 여 리소스 경합 방지 하려면.

연결 된 특정 R 기본 패키지 배포 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스는 인스턴스와 연결 된 폴더에서 찾을 수 있습니다. 예를 들어 R 서비스 기본 인스턴스를 설치한 경우 R 라이브러리에 있는 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`합니다.

마찬가지로, 기본 인스턴스와 연결 된 R 도구는에 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`,

기본 배포에 대 한 자세한 내용은 참조 [Microsoft R Open과 설치 된 패키지](https://mran.revolutionanalytics.com/rro/installed/)

### 추가 R 패키지

기본 R 분포 외에도 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] R 및 실행을 지 원하는 R의 원격 계산 컨텍스트에서 라이브러리의 병렬 실행을 위한 프레임 워크 뿐만 아니라 일부 독점 R 패키지가 포함 되어 있습니다. 

이 조합 된 기능 집합을 R-R 기본 배포와 향상 된 R 기능 및 패키지-라고 **Microsoft R**합니다. Microsoft R 서버 (독립 실행형)를 설치 하는 경우 동일한 일련을의 SQL Server R 서비스 (데이터베이스)를 사용 하지만 다른 폴더에 설치 된 패키지를 얻습니다. 

Microsoft R 신속한 수학 처리를 가능 하면 사용 되는 Intel 수학 커널 라이브러리의 분포를 포함 합니다. 예를 들어 기본 선형 대 수 (BLAS) 라이브러리는 다양 한 R 자체의 경우와 추가 기능 패키지에 사용 됩니다. 자세한 내용은 다음이 문서를 참조 합니다.

+ [Intel 수학 커널 R 빨라집니다 하는 방법](http://blog.revolutionanalytics.com/2014/10/revolution-r-open-mkl.html)
+ [다중 스레드 수학 라이브러리에 연결 하는 R의 성능 이점](http://blog.revolutionanalytics.com/2010/06/performance-benefits-of-multithreaded-r.html)

Microsoft R에 대 한 가장 중요 한 추가 중에 **RevoScaleR** 및 **RevoPemaR** 패키지 합니다. 이들은 C 또는 c + +에서 주로 성능 향상을 위해 기록 된 R 패키지입니다.

+ **RevoScaleR 합니다.** 다양 한 Api 데이터 조작 및 분석을 위해 포함 됩니다. Api는 메모리에 맞지 않는 및 여러 코어 또는 프로세서가 통해 배포 하는 계산을 수행 하기에 너무 큰 데이터 집합을 분석할 때 최적화 합니다.

   또한 RevoScaleR Api 확장성에 대 한 데이터의 하위 집합에 대 한 작업을 지원 합니다. 즉, 대부분의 RevoScaleR 함수는 데이터 및 집계 결과를 업데이트 하는 알고리즘을 사용 하 여 청크에서 작동할 수 있습니다. 따라서 RevoScaleR 함수를 기반으로 하는 R 솔루션 매우 큰 데이터 집합으로 작업할 수 있으며 로컬 메모리에 바인딩되지 않습니다.

  RevoScaleR 패키지도 지원 합니다.는 합니다. XDF 빠르게 이동 및 분석을 위해 사용 되는 데이터 저장소에 대 한 파일 형식입니다. XDF 형식 종형 저장을 사용 하 여는 이식 가능 및 로드 하 고 텍스트, SPSS, 또는 ODBC 연결을 비롯 한 다양 한 원본의 데이터를 조작 하는 데 사용 될 수 있습니다. 이 자습서에서는 XDF 형식을 사용 하는 방법의 예를 제공 합니다. [데이터 과학에 대 한 심층 정보](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)


+ **RevoPemaR 합니다.** PEMA는 외부 메모리 알고리즘을 병렬를 나타냅니다.  **RevoPemaR** 패키지는 사용자 고유의 병렬 알고리즘을 개발 하는 데 사용할 수 있는 Api를 제공 합니다. 자세한 내용은 참조 [RevoPemaR 시작 가이드](https://msdn.microsoft.com/microsoft-r/rserver/rserver-pemar-getting-started)합니다.

## 참고 항목
[아키텍처 개요](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)

[R 서비스를 지 원하는 SQL Server의 새로운 구성 요소](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)

[보안 개요](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)
