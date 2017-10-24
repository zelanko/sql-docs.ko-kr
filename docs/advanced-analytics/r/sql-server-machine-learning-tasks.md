---
title: "작업을 학습 하는 SQL Server 컴퓨터 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: c0e7a0929d5caa84df1a1fb02894db08313a36bd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/06/2017

---
# <a name="sql-server-machine-learning-tasks"></a>SQL Server 기계 학습 작업

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 는 데이터 저장 및 관리, 워크플로 개발, 보고 및 시각화를 위한 엔터프라이즈 수준의 도구와 오픈 소스 R 언어의 강력함 및 유연성을 결합합니다. 이 항목에서는 기계 학습, 그 SQL Server enagged 기계 학습에서 하는 4 명의 서로 다른 데이터 전문가의 요구를 지원 하는 방법을 설명 합니다.

## <a name="machine-learning-life-cycle"></a>기계 학습 수명 주기

기계 학습 단기 작업 아니라 모든 측면의 기업에서 데이터를 사용 하는 장기 프로세스 대신입니다. 기계 학습의 비즈니스 목표와 규칙을 식별 및 센서 및 비즈니스 응용 프로그램에서 데이터 수집을 시작합니다. 기계 학습 추출, 처리 및 데이터를 저장 하기 위한 프로세스에 따라 및 저장, 추출 및 감사 데이터에 대 한 정책을 고려 하는 경우에 점점 더 중요 합니다. 마지막으로, 기계 학습 보고 및 분석 뿐만 아니라 고객 참여 및 피드백에 대 한 전략의 중요 한 omponent 되었습니다.



SQL Server 기계 학습에 맞지 않으므로 다양 한 기계 학습 프로세스의에서 간격 연결:

+ 작동 하는 온-프레미스 또는 클라우드에서
+ Business intelligence를 비롯 한 엔터프라이즈 데이터 처리의 각 단계에서 통합
+ 에서는 향상 된 데이터 보안
+ 리소스 관리 및 감사를 제공합니다.

## <a name="data-professionals-and-how-they-use-machine-learning"></a>데이터 전문가 및 방법을 사용 하 여 기계 학습 있습니다

### <a name="data-scientists"></a>데이터 과학자

데이터 과학자는 여러 가지 도구에 대 한 액세스 데이터 분석 및 기계 학습, Excel 또는 무료 오픈 소스 플랫폼에서 심층 기술적 지식이 필요한 고가의 통계 제품군 까지입니다. 그러나 SQL Server와 통합 특유의 이점을 제공합니다.

+ 원하는 R 개발 환경을 사용하여 솔루션 개발 및 테스트
+ 엔터프라이즈 보안 정책을 준수 하는 동안 데이터 이동을 방지 데이터베이스에 계산을 푸시하십시오.
+ 특별 한 R 패키지와 Api를 통해 성능 및 확장성 개선 되었습니다. 더 이상 r을 단일 스레드, 메모리 집중형 아키텍처에 의해 제한 되 고 큰 데이터 집합 및 다중 스레드, 다중 코어 및 다중 프로세스 계산을 작업할 수 없습니다.
+ R 코드를 쉽게 프로덕션 환경에 배포 및 엔터프라이즈 도구, 응용 프로그램, 다른 데이터베이스 및 대시보드를 호출한 수 있습니다.
+ 데이터 과학자를 배포 하 고 보안 및 액세스 감사를 비롯 한 엔터프라이즈 데이터 관리에 대 한 표준 요구 사항을 충족 하면서 분석 솔루션을 업데이트할 수 있습니다.
+ 코드 이식성: 쉽게 다시 R 코드를 Hadoop 등의 다른 데이터 원본 사용

### <a name="application-and-database-developers"></a>응용 프로그램 및 데이터베이스 개발자

데이터베이스 개발자는 여러 기술을 통합하고 엔터프라이즈 전체에서 공유할 수 있도록 통합 결과를 취합합니다. 그리고 응용 프로그램 개발자, SQL 개발자 및 데이터 과학자와 협력하여 솔루션을 설계하고 권장 데이터 관리 방법을 제시하고 솔루션을 구축/배포합니다. 

SQL Server와의 통합에는 기계 학습을 사용 하는 데이터 개발자에 게 이러한 이점을 제공 합니다.

+ 친숙 한 도구를 사용 하 여 R 스크립트와 상호 작용할 수 있습니다. 데이터 개발자 SQL Server Management Studio를 사용 하 여 솔루션을 배포 하는 동안 RStudio에서 작업 하는 데이터 과학자가 있습니다. Python 또는 R 솔루션의 기록이 더 이상 없습니다.
+ 조건과 SQL 및 R, 또는 SQL 및 Python을 혼합 하 여 최적화 합니다. 여러 번 큰 데이터 집합에서 복잡 한 작업 실행할 수 있습니다 훨씬 더 효율적으로 메모리에 columnstoreindexes 또는 매우 빠른 집계 등의 SQL Server 기능을 사용 하 여 T-SQL에서. 기계 학습 언어 적절를 사용 하 고 SQL으로 이동 하 고 데이터를 처리 합니다.
+ 손쉽게 대량의 프로덕션 데이터에 대 한 예측 점수 생성 등의 데이터에 반복적으로 실행 해야 하는 작업을 자동화 합니다.
+ 사용 하는 모든 응용 프로그램에서 R, Python 스크립트 실행 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. 매개 변수가 있는 모델을 만드는, 복잡 한 플롯을 생성 하거나 예측을 출력 하는 저장된 프로시저를 호출 하기만 됩니다.
+ **RevoScaleR** 및 **revoscalepy** Api는 큰 데이터 집합에 작동 하 고 다중 스레드, 다중 코어 및 다중 프로세스 데이터베이스 내 계산에서 이점을 얻을 수 있습니다.

관련된 작업에 대 한 자세한 내용은 다음을 참조 하세요.
+ [Operationalizing Your R Code](../../advanced-analytics/r-services/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>데이터베이스 관리자

데이터베이스 관리자는 경쟁 프로젝트와 우선 순위를 단일 연락 지점 즉, 데이터베이스 서버로 통합해야 합니다. 이들은 운영 및 보고 데이터 저장소의 상태를 유지하면서 데이터 과학자뿐만 아니라 다양한 보고서 개발자, 비즈니스 분석가, 비즈니스 데이터 소비자에게 데이터 액세스를 제공해야 합니다. 엔터프라이즈에서 DBA는 데이터 과학을 위한 효과적인 인프라를 구축하고 배포하는 핵심적인 부분입니다. 

SQL Server는 데이터 과학 임무를 지원 해야 하는 데이터베이스 관리자에 대 한 고유한 기능을 제공 합니다.

+ SQL Server에서 보안:의 아키텍처 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 데이터베이스의 보안을 유지 하 고 데이터베이스 인스턴스의 작업에서 세션 외부 스크립트 실행을 격리 합니다. 데이터베이스 역할을 사용 하 여 새 R 패키지를 설치할 수 있는 사용자 및 컴퓨터 학습 스크립트를 실행할 수 있는 권한이 있는 사용자를 지정할 수 있습니다.

+ R 및 Python 세션 외부 스크립트에 문제가 발생 하는 경우에 일반적으로 실행 하 여 서버 계속 되도록 하기 위해서 별도 프로세스에서 실행 됩니다.

+ SQL Server를 사용 하 여 리소스 관리를 사용 하면 메모리 및 대규모 계산이 서버의 전반적인 성능을 저해를 방지 하기 위해 외부 런타임에 할당 하는 프로세스를 제어할 수 있습니다.

관련된 작업에 대 한 자세한 내용은 다음을 참조 하세요.
+ [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

### <a name="architects-and-etl-designers"></a>설계자 및 ETL 디자이너

설계자는 컴퓨터 학습 수명 주기의 모든 측면을 포괄 하는 통합된 워크플로 설계 합니다. 데이터 엔지니어 디자인 및 ETL 솔루션을 구축 및 최적화 기능 엔지니어링 하는 방법을 결정 합니다. 기계 학습 프로세스의 일부인 동시 작업 합니다. 종종 전체 데이터 플랫폼 경쟁 하 고 보완 비즈니스 요구를 균등화를 위해 디자인 되어야 합니다.

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 비즈니스 인텔리전스, 데이터 웨어하우스 스택, 엔터프라이즈 클라우드 및 이동성 도구, Hadoop과 같은 다른 Microsoft 도구와 긴밀하게 통합되어 있기 때문에 고급 분석을 도모하려는 데이터 엔지니어나 시스템 설계자에게 다수의 이점을 제공합니다.

+ Python 및 R 솔루션을 개발 하기 위한 친숙 한 개발 도구입니다. 데이터 집합을 채우거 나 그래픽을 생성 하거나 예측을 확보 시스템 저장 프로시저를 사용 하 여 모든 Python 또는 R 스크립트를 호출할 수 있습니다. 없습니다 자세한 디자인에서 병렬 워크플로 데이터 과학 및 ETL 도구입니다. Azure 데이터 팩터리 및 Azure SQL 데이터베이스에 대 한 지원을 사용 하면 보다 쉽게 변환 하 고 데이터를 관리 및 기계 학습 워크플로에에서 클라우드 데이터 원본을 사용 합니다.

+ 예약 및 Microsoft R server에서 화 기능을 사용 하 여 관리 합니다.

관련된 작업에 대 한 자세한 내용은 다음을 참조 하세요.

+ [SQL Server에서 R을 사용하는 워크플로 만들기](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)


