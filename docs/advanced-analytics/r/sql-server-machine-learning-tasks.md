---
title: 수명 주기 및 팀 프로세스 학습 컴퓨터 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ca7d0acf3097ec031cba5f3a7245d5594b7927bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="machine-learning-lifecycle-and-personas"></a>가상 사용자 및 컴퓨터 학습 수명 주기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

기술 및 전문가의 서로 다른 집합의 공동 작업을 필요 하기 때문에 컴퓨터 학습 프로젝트 복잡할 수 있습니다. 이 문서에서는 기계 학습 및 SQL Server 요구를 지원 하는 방법에 관련 된 데이터 전문가 유형의 시스템 학습 주기에서 주 작업 설명입니다.

> [!TIP]
> 
> 기계 학습 프로젝트를 시작 하기 전에 도구 및에서 제공 하는 모범 사례를 검토 하는 것이 좋습니다는 [Microsoft 팀 데이터 과학 프로세스](https://blogs.technet.microsoft.com/machinelearning/2017/10/09/the-microsoft-team-data-science-process-tdsp-recent-updates/), 또는 TDSP 합니다. 기계 학습 컨설턴트 계획 하 고 기계 학습 프로젝트에서 반복에 대 한 모범 사례를 통합 하는 microsoft에서이 프로세스를 만들었습니다. TDSP CRISP-DM, 등 업계 표준에서에 해당 루트가 하지만 DevOps 및 시각화와 같은 최근 사례를 통합 합니다.

## <a name="machine-learning-life-cycle"></a>컴퓨터 학습 수명 주기

기계 학습 모든 측면의 기업에서 데이터를 사용 하는 복잡 한 프로세스 이며 많은 컴퓨터 학습 프로젝트 더 오래 걸린 것으로 예상 보다 더 복잡 한 되 고 종료 합니다. 다음은 일부의 기계 학습 기업에서 데이터 전문가 지원 해야 하는 방법입니다.

+ 기계 학습 목표 및 비즈니스 규칙의 id로 시작합니다.
+ 컴퓨터 학습 전문가 저장, 추출 및 감사 데이터에 대 한 정책 알고 있어야 합니다.
+ 다음 잠재적으로 적용할 수 있는 데이터의 컬렉션이입니다.  데이터 소스를 식별 하 고 센서 및 비즈니스 응용 프로그램에서 적절 한 데이터 추출 합니다. 
+ 시스템 학습 활동의 품질은 뿐 아니라 데이터를 사용할 수는 있지만 추출, 처리 및 데이터 저장에 사용 되는 매우 프로세스의 형식에 따라 크게 달라 집니다. 
+ 기계 학습 프로젝트 없음이 보고 및 분석 하 고 가능한 고객 참여 및 피드백에 대 한 전략 없이 완성 됩니다.

SQL Server는 다양 한 엔터프라이즈 데이터 전문가 및 컴퓨터 학습 전문가 간의 간격을 브리징 하는 데 도움이 됩니다.

+ 데이터 저장된 온-프레미스 가능 또는 클라우드
+ ETL 및 보고를 비롯 한 엔터프라이즈 데이터 처리의 각 단계에서 SQL Server 통합
+ SQL Server 지원 데이터 보안, 데이터 중복성 및 감사
+ 리소스 관리를 제공합니다.

## <a name="data-scientists"></a>데이터 과학자

데이터 과학자는 데이터 분석 및 기계 학습, Excel 또는 무료 오픈 소스 플랫폼에서 심층 기술적 지식이 필요한 고가의 통계 제품군에 이르기까지에 여러 가지 도구를 사용 합니다. 그러나 R, Python을 사용 하 여 SQL Server와 함께 이러한 기존 도구에 비하면 몇 가지 특유의 이점을 제공 합니다.

+ 개발 하 고 T-SQL 코드의 일부로 R, Python 코드를 배포의 선택한 개발 환경을 사용 하 여 솔루션을 테스트할 수 있습니다.
+ 데이터 과학자 랩톱 off 및 엔터프라이즈 보안 정책을 충족 하기 위해 데이터를 이동 하지 않고 서버에 복잡 한 계산을 이동 합니다.
+ 특별 한 R 패키지와 Api를 통해 성능 및 확장성 개선 되었습니다. 더 이상 r을 단일 스레드, 메모리 집중형 아키텍처에 의해 제한 되 고 큰 데이터 집합 및 다중 스레드, 다중 코어 및 다중 프로세스 계산을 작업할 수 없습니다.
+ 코드 이식성: 솔루션에서 Hadoop 또는 Linux를 SQL Server에서 실행할 수를 사용 하 여 [컴퓨터 학습 서버](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)합니다. 코드를 한 번, 원하는 위치에 배포 합니다.

## <a name="application-and-database-developers"></a>응용 프로그램 및 데이터베이스 개발자

데이터베이스 개발자는 여러 기술을 통합하고 엔터프라이즈 전체에서 공유할 수 있도록 통합 결과를 취합합니다. 데이터베이스 개발자는 솔루션을 디자인, 권장 데이터 관리 방법 및 설계자 또는 솔루션을 배포 하는 응용 프로그램 개발자, SQL 개발자 및 데이터 과학자와 작업 합니다.

SQL Server와의 통합 데이터 개발자에 게 많은 이점을 제공합니다.

+ 데이터 개발자 SQL Server Management Studio를 사용 하 여 솔루션을 배포 하는 동안 데이터 과학자 RStudio에서 작업할 수 있습니다. Python 또는 R 솔루션의 기록이 더 이상 없습니다.
+ T-SQL, R, 및 Python의 사용 하 여 솔루션을 최적화 합니다. 훨씬 더 효율적으로 사용 하 여 보다 SQL Server 데이터베이스 전문가 대 한 정보가 오른쪽 활용에 메모리 내 columnstore 인덱스를 사용 하 여 컴퓨터 학습 솔루션의 성능을 개선 하기 위해 큰 데이터 집합에서 복잡 한 작업을 실행할 수 있습니다 및 SQL 집합 기반 작업을 사용 하 여 집계 합니다. 
+ 손쉽게 대량의 프로덕션 데이터에 대 한 예측 점수 생성 등의 데이터에 반복적으로 실행 해야 하는 작업을 자동화 합니다. 
+ 액세스를 사용 하는 모든 응용 프로그램에서 R, Python 스크립트 매개 변수가 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. 모델을 학습, 플롯을 생성 하거나 예측을 출력 하는 저장된 프로시저를 호출 하기만 됩니다.
+ Api는 큰 데이터 집합을 스트림 하 고 다중 스레드, 다중 코어 및 다중 프로세스 데이터베이스 내 계산에서 이점을 얻을 수 있습니다.

관련된 작업에 대 한 자세한 내용은 다음을 참조 하세요.
+ [작업에서 R 코드 활용](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>데이터베이스 관리자

데이터베이스 관리자는 경쟁 프로젝트와 우선 순위를 단일 연락 지점 즉, 데이터베이스 서버로 통합해야 합니다. 이들은 운영 및 보고 데이터 저장소의 상태를 유지하면서 데이터 과학자뿐만 아니라 다양한 보고서 개발자, 비즈니스 분석가, 비즈니스 데이터 소비자에게 데이터 액세스를 제공해야 합니다. 엔터프라이즈에서 DBA는 데이터 과학을 위한 효과적인 인프라를 구축하고 배포하는 핵심적인 부분입니다. 

SQL Server는 데이터 과학 임무를 지원 해야 하는 데이터베이스 관리자에 대 한 고유한 기능을 제공 합니다.

+ SQL Server에서 보안:의 아키텍처 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 데이터베이스의 보안을 유지 하 고 데이터베이스 인스턴스의 작업에서 세션 외부 스크립트 실행을 격리 합니다. 컴퓨터 학습 스크립트를 실행 하 고 데이터베이스 역할을 사용 하 여 패키지를 관리 하려면 권한이 있는 사용자를 지정할 수 있습니다.

+ R 및 Python 세션 외부 스크립트에 문제가 발생 하는 경우에 일반적으로 실행 하 여 서버 계속 되도록 하기 위해서 별도 프로세스에서 실행 됩니다.

+ SQL Server를 사용 하 여 리소스 관리를 사용 하면 메모리 및 대규모 계산이 서버의 전반적인 성능을 저해를 방지 하기 위해 외부 런타임에 할당 하는 프로세스를 제어할 수 있습니다.

관련된 작업에 대 한 자세한 내용은 다음을 참조 하세요.
+ [기계 학습 솔루션 관리 및 모니터링](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>설계자와 데이터 엔지니어

설계자는 컴퓨터 학습 수명 주기의 모든 측면을 포괄 하는 통합된 워크플로 설계 합니다. 데이터 엔지니어 디자인 및 ETL 솔루션을 빌드하고 기계 학습에 대 한 기능 엔지니어링 작업을 최적화 하는 방법을 결정 합니다. 전체 데이터 플랫폼 경쟁 비즈니스 요구를 균등화를 위해 디자인 되어야 합니다.

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 비즈니스 인텔리전스, 데이터 웨어하우스 스택, 엔터프라이즈 클라우드 및 이동성 도구, Hadoop과 같은 다른 Microsoft 도구와 긴밀하게 통합되어 있기 때문에 고급 분석을 도모하려는 데이터 엔지니어나 시스템 설계자에게 다수의 이점을 제공합니다.

+ 데이터 집합을 채우거 나 그래픽을 생성 하거나 예측을 확보 시스템 저장 프로시저를 사용 하 여 모든 Python 또는 R 스크립트를 호출 합니다. 없습니다 자세한 디자인에서 병렬 워크플로 데이터 과학 및 ETL 도구입니다. Azure 데이터 팩터리 및 Azure SQL 데이터베이스에 대 한 지원 하기가 쉬워집니다 기계 학습 워크플로에에서 클라우드 데이터 원본을 사용 합니다.

+ 일정 예약 및 기계 학습 작업의 관리에 대 한 SQL server에서 Integration Services, SQL 에이전트, 또는 Azure Data Factory에 따라 표준 자동화 워크플로 사용 합니다. 또는 사용 하 여는 [해결해줍니다 기능](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r) 학습 서버 컴퓨터에에서 있습니다.

관련된 작업에 대 한 자세한 내용은 다음을 참조 하세요.

+ [SQL Server의 시스템 학습 워크플로 만들기](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)

