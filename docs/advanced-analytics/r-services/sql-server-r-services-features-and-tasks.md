---
title: "SQL Server R Services 기능 및 태스크 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 13
---
# SQL Server R Services 기능 및 태스크
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 강력 함과 유연성 오픈 소스 R 언어의 데이터 저장 및 관리, 워크플로 개발 하 고 보고 및 시각화를 위한 엔터프라이즈 수준의 도구와 결합합니다. 4 가지 데이터 전문가 및 시나리오의 요구를 지원합니다.  
  
## 데이터 과학자: R 및 SQL Server를 사용하여 분석, 모델링, 점수 매기기  
 데이터 과학자는 친숙한 Excel이나 오픈 소스 플랫폼에서부터 해박한 기술적 지식이 필요한 고가의 통계 제품군에 이르는 다양한 데이터 분석 및 기계 학습 도구를 사용할 수 있습니다. 그 중 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 는 데이터 과학자가 데이터를 이동하지 않고 엔터프라이즈 보안 정책을 준수하면서 데이터베이스에 계산을 푸시할 수 있다는 특유의 이점을 제공합니다. 또한 데이터 과학자가 생성한 R 코드를 프로덕션에 손쉽게 배포할 수 있고 친숙한 엔터프라이즈 도구 및 솔루션( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스, BI 보고 도구, 대시보드 기반 응용 프로그램)에서 호출할 수 있습니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 사용하여, 데이터 과학자는 보안, 손쉬운 배포, 관리 및 모니터링, 액세스 감사를 비롯한 엔터프라이즈 데이터 관리에 대한 표준 요구 사항을 충족하면서 분석 솔루션을 배포하고 업데이트할 수 있습니다.  
  
-   **친숙한 사용자 인터페이스**  원하는 R 개발 환경을 사용하여 솔루션 개발 및 테스트  
  
-   **In-Database 처리**  R 코드를 실행 하 고 호스팅하는 컴퓨터에서 수행 하는 계산 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스. 이렇게 하면 데이터를 이동할 필요가 없습니다.  
  
-   **뛰어난 성능과 확장성.**  확장 가능한 R 패키지 및 Api와 구입 R.의 단일 스레드, 메모리 집중형 아키텍처에는 더 이상이 제한 되어 있으므로 큰 데이터 집합 및 다중 스레드, 다중 코어 및 다중 프로세스 계산 작업할 수 있습니다.  
    
-   **코드 이식성**  에 대해 실행 되는 동일한 R 코드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터는 Hadoop과 같은 다른 데이터 원본에 대해 쉽게 다시 사용할 수 있습니다.  
  
 관련된 작업 및 개념에 대 한 자세한 내용은 참조 하십시오. [데이터 탐색 및 R로 예측 모델링](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)합니다.  
  
## 응용 프로그램 및 데이터베이스 개발자: R 솔루션 배포  
 데이터베이스 개발자는 여러 가지 기술을 통합하여 엔터프라이즈에서 두루 공유할 수 있도록 그 결과를 모으는 태스크를 담당합니다. 데이터베이스 개발자는 솔루션을 설계하고, 데이터 관리 방법을 추천하고, 솔루션을 기획 및 배포하기 위해 응용 프로그램 개발자, SQL 개발자, 데이터 과학자와 협력합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 는 데이터 과학자와 작업하는 개발자들에게 많은 이점을 제공합니다.  
  
-   **R 스크립트를 사용 하 여 상호 작용할 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다.**  보고서 개발자, 분석가, 데이터베이스 개발자는 시스템 저장 프로시저를 호출하여 R 스크립트를 호출할 수 있습니다. 솔루션에 복잡 한 집계를 사용 하 여 또는 큰 데이터 집합을 포함 하는 경우에 데이터베이스에서 실행 하거나 R의 조합을 사용 하 여 계산을 할 수 있습니다 및 [!INCLUDE[tsql](../../includes/tsql-md.md)], 최상의 성능을 제공 하는에 따라 합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 와(과)의 손쉬운 통합은 프로덕션 데이터에 대한 예측 점수 생성과 같이 대량의 데이터에 반복적으로 태스크를 실행해야 하는 경우에 매우 유용합니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와(과) 통합하면 [!INCLUDE[tsql](../../includes/tsql-md.md)]을(를) 사용하는 모든 응용 프로그램에서 R 스크립트를 실행할 수 있습니다. 예를 들어에서 저장된 프로시저를 쉽게 호출할 수는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 R 스크립트를 호출 하는 보고서에 예측 함께 도표를 생성 합니다.  
  
-   **뛰어난 성능과 확장성.**  RevoScaleR 패키지 Api에서 제공 되는 오픈 소스 R 언어 제한 사항이에 알려져 있지만 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 큰 데이터 집합에 작동 하며 다중 스레드, 다중 코어 및 다중 프로세스에 해당 하는 데이터베이스에서의 계산에서 이점을 얻을 수 있습니다.  
  
-   **표준 개발 및 관리 도구.**  관리나 개발을 위한 도구가 추가로 필요하지 않습니다. 모든 R 작업은 저장 프로시저를 호출하여 호출할 수 있습니다. 뿐만 아니라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터에 대해 실행하는 것과 같은 R 코드를 Hadoop 등의 다른 데이터 원본에 사용할 수도 있습니다.  
  
 관련된 작업 및 개념에 대 한 자세한 내용은 참조 하십시오. [R 코드 운용성](../../advanced-analytics/r-services/operationalizing-your-r-code.md)합니다.  
  
## 데이터베이스 관리자: 고급 분석 솔루션 관리  
 데이터베이스 관리자는 경쟁 프로젝트와 우선 순위를 단일 연락 지점 즉, 데이터베이스 서버로 통합해야 합니다. 이들은 운영 및 보고 데이터 저장소의 상태를 유지하면서 데이터 과학자뿐만 아니라 다양한 보고서 개발자, 비즈니스 분석가, 비즈니스 데이터 소비자에게 데이터 액세스를 제공해야 합니다. 엔터프라이즈에서 DBA는 데이터 과학을 위한 효과적인 인프라를 구축하고 배포하는 핵심적인 부분입니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 는 데이터 과학 임무를 지원하는 데이터베이스 관리자에게 많은 이점을 제공합니다.  
  
-   **보안.**  아키텍처 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 데이터베이스 보안을 유지 하 여 데이터베이스 인스턴스의 작업에서 R 세션의 실행을 격리 합니다.  
  
     R 스크립트를 실행 하에 정의 된 동일한 보안 역할을 사용 하 여 R 작업에 사용 되는 데이터는 관리 권한이 있는 사용자를 지정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
-   **안정성.**  R 세션은 R 세션에 문제가 발생하더라도 서버가 평상시처럼 계속 실행되도록 하기 위해서 별도의 프로세스로 실행됩니다.  
  
-   **리소스 관리.**  대규모 계산이 서버의 전반적인 성능을 저해하지 않도록 R 런타임에 할당된 리소스 양을 제어할 수 있습니다.  
  
 관련 태스크 및 개념에 대한 자세한 내용은 [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)을(를) 참조하세요.  
  
## 설계자 및 ETL 디자이너: R 및 SQL Server를 포괄하는 통합 워크플로 만들기  
 데이터 엔지니어는 ETL 솔루션을 디자인하고 구축합니다. 설계자는 서로 상충하고 보완하는 비즈니스 요구를 수용하는 데이터 플랫폼을 설계합니다. 때문에 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 강력 하 게 통합 되는 비즈니스 인텔리전스 및 데이터 웨어하우스 스택, 엔터프라이즈 클라우드 및 모바일 도구 및 Hadoop와 같은 다른 Microsoft 도구와 고급 분석을 승격 하려는 데이터 엔지니어 또는 시스템 설계자에 혜택의 배열을 제공 합니다.  
  
-   **폭넓고 친숙한 개발 도구**  R 솔루션 개발 시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 와 시스템 저장 프로시저를 사용하여 데이터 집합을 채우거나 R 작업을 실행하거나 예측을 확보합니다. 데이터 과학 도구에서 병렬 워크플로를 디자인할 필요가 없습니다. 친숙한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]환경에서 자신만의 데이터 파이프라인을 구축하세요.  
  
     클라우드 데이터 사용 Azure 데이터 팩터리 및 Azure SQL 데이터베이스에 대 한 지원을 쉽게 변환 하는 데이터를 관리 하 고 온-프레미스에 대 한 정당한 워크플로에서 사용 하 여 클라우드 데이터 원본을 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터입니다.  
  
-   **워크플로 작성 및 관리**  작업 및 시스템 저장 프로시저를 사용 하 여 R 스크립트를 포함 하는 만든 워크플로 예약 합니다.  
  
 관련된 작업 및 개념에 대 한 자세한 내용은 참조 하십시오. [만들기 워크플로 SQL Server에서 사용 하 여 R](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)합니다.  
  
## 참고 항목  
 [SQL Server R Services 시작하기](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  