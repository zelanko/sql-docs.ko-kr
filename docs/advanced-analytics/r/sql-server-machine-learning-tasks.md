---
title: 기계 학습 수명 주기 및 팀 프로세스-SQL Server Machine Learning 서비스
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4d19c103f2e90220bc7d80a1da65eb0352252ad6
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511290"
---
# <a name="machine-learning-lifecycle-and-personas"></a>Machine learning 수명 주기 및 사용자
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Machine learning 프로젝트 기술 및 전문가의 서로 다른 집합의 공동 작업에 필요 하므로 복잡할 수 있습니다. 이 문서에서는 machine learning 수명 주기에서 machine learning 및 SQL Server 요구를 지원 하는 방법에 참여 하는 데이터 전문가의 형식 주체 작업을 설명 합니다.

> [!TIP]
> 
> Machine learning 프로젝트에서 시작 하기 전에 도구 및에서 제공 하는 모범 사례를 검토 하는 것이 좋습니다 합니다 [Microsoft Team Data Science Process](https://blogs.technet.microsoft.com/machinelearning/2017/10/09/the-microsoft-team-data-science-process-tdsp-recent-updates/), 또는 TDSP 합니다. 이 프로세스는 기계 학습 계획 및 반복 기계 학습 프로젝트에 대 한 모범 사례를 통합 하는 microsoft 컨설턴트에서 작성 되었습니다. TDSP은 CRISP-DM와 같은 업계 표준의 해당 루트를 갖지만 DevOps 및 시각화와 같은 최신 사례를 통합 합니다.

## <a name="machine-learning-life-cycle"></a>Machine learning 수명 주기

Machine learning은 기업에서 데이터의 모든 측면에 영향을 주는 복잡 한 프로세스 및 여러 machine learning 프로젝트 오래 예상한 것 보다 더 복잡 한 되 고 종료 합니다. 일부의 기계 학습 엔터프라이즈의 데이터 전문가의 지원이 필요는 다음과 같습니다.

+ 기계 학습 목표와 비즈니스 규칙의 id를 사용 하 여 시작합니다.
+ Machine learning 전문가 저장, 추출 및 감사 데이터에 대 한 정책 인식 해야 합니다.
+ 다음 잠재적으로 적용할 수 있는 데이터의 컬렉션이입니다.  데이터 소스를 식별 해야 하 고 센서 및 비즈니스 응용 프로그램에서 적절 한 데이터를 추출 합니다. 
+ Machine learning 작업의 품질을 사용할 수 있는 데이터의 추출, 처리 및 데이터 저장에 사용 되는 매우 프로세스 형식 뿐만 아니라 매우 달라 집니다. 
+ Machine learning 프로젝트가 없어서는 안 보고 및 분석 하 고 가능한 경우 고객 및 피드백에 대 한 전략입니다.

SQL Server는 다양 한 엔터프라이즈 데이터 전문가 및 기계 학습 전문가 간의 격차를 극복 하는 데 도움이 됩니다.

+ 데이터는 온-프레미스로 저장된 될 수 있습니다 또는 클라우드에서
+ ETL 및 엔터프라이즈 데이터 처리, 보고 등의 모든 단계에서 SQL Server 통합
+ SQL Server는 데이터 보안, 데이터 중복성 및 감사 지원
+ 리소스 거 버 넌 스를 제공합니다.

## <a name="data-scientists"></a>데이터 과학자

데이터 과학자는 데이터 분석 및 machine learning, Excel 또는 무료 오픈 소스 플랫폼에서 깊이 있는 기술 지식이 필요한 고가의 통계 제품군에 이르기까지 다양 한 도구를 사용 합니다. 그러나 SQL Server를 사용 하 여 R 또는 Python을 사용 하 여 이러한 기존 도구에 비해 몇 가지 고유한 이점을 제공 합니다.

+ 개발 하 고 원하는 개발 환경을 사용 하 여 솔루션을 테스트 다음 T-SQL 코드의 일부로 R 또는 Python 코드를 배포할 수 있습니다.
+ 데이터 과학자의 랩톱 해제 하 고 엔터프라이즈 보안 정책을 준수 하기 위해 데이터 이동을 방지할 서버로 복잡 한 계산을 이동 합니다.
+ 특별 한 R 패키지 및 Api를 통해 성능 및 확장성 개선 되었습니다. 더 이상 단일 스레드, 메모리 집중형 R 아키텍처에 의해 제한 됩니다 하 고 큰 데이터 집합 및 다중 스레드, 다중 코어 및 다중 프로세스 계산이 가능 작업할 수 없습니다.
+ 코드 이식성: 솔루션 또는 Hadoop 또는 Linux에서 SQL Server에서 실행할 수 있습니다 사용 하 여 [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)합니다. 코드를 한 번, 어디서 나 배포.

## <a name="application-and-database-developers"></a>응용 프로그램 및 데이터베이스 개발자

데이터베이스 개발자는 여러 기술을 통합하고 엔터프라이즈 전체에서 공유할 수 있도록 통합 결과를 취합합니다. 데이터베이스 개발자는 솔루션을 디자인, 데이터 관리 방법을 권장 하 고 설계 또는 솔루션을 배포 하는 응용 프로그램 개발자, SQL 개발자 및 데이터 과학자를 사용 하 여 작동 합니다.

SQL Server와의 통합 데이터 개발자에 게 많은 이점을 제공합니다.

+ 데이터 과학자가 데이터 개발자는 SQL Server Management Studio를 사용 하 여 솔루션을 배포 하는 동안 RStudio에서 작업할 수 있습니다. 더 이상 다시 코딩 하는 R 또는 Python 솔루션입니다.
+ T-SQL, R 및 Python의 가장을 사용 하 여 솔루션을 최적화 합니다. 훨씬 더 효율적으로 사용 하 여 SQL Server R. 활용 하면 데이터베이스 전문가의 지식에에서 메모리 내 columnstore 인덱스를 사용 하 여 기계 학습 솔루션의 성능을 개선 하기 위해 큰 데이터 집합에서 복잡 한 작업을 실행할 수 있습니다 및 SQL 집합 기반 작업을 사용 하 여 집계 합니다. 
+ 간편 하 게 많은 양의 프로덕션 데이터에 대 한 예측 점수 생성 등의 데이터에 반복적으로 실행 해야 하는 작업을 자동화 합니다. 
+ 액세스를 사용 하는 모든 응용 프로그램에서 R 또는 Python 스크립트를 매개 변수화 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. 모델을 학습 하 고, 플롯을 생성 또는 예측을 출력 하는 저장된 프로시저를 호출 하기만 됩니다.
+ Api는 큰 데이터 집합을 스트림 하 고 다중 스레드, 다중 코어 및 다중 프로세스 데이터베이스 내 계산에서 이점을 얻을 수 있습니다.

관련된 태스크에 대 한 내용은 다음을 참조 하세요.
+ [R 코드 운영 화](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>데이터베이스 관리자

데이터베이스 관리자는 경쟁 프로젝트와 우선 순위를 단일 연락 지점 즉, 데이터베이스 서버로 통합해야 합니다. 이들은 운영 및 보고 데이터 저장소의 상태를 유지하면서 데이터 과학자뿐만 아니라 다양한 보고서 개발자, 비즈니스 분석가, 비즈니스 데이터 소비자에게 데이터 액세스를 제공해야 합니다. 엔터프라이즈에서 DBA는 데이터 과학을 위한 효과적인 인프라를 구축하고 배포하는 핵심적인 부분입니다. 

SQL Server 데이터 과학 임무를 지원 해야 하는 데이터베이스 관리자에 대 한 고유한 기능을 제공 합니다.

+ SQL Server에서 보안: 아키텍처 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 데이터베이스의 보안을 유지 하 고 실행을 외부 스크립트 세션 데이터베이스 인스턴스 작업과에서 격리 시킵니다. 기계 학습 스크립트를 실행 하 여 데이터베이스 역할을 사용 하 여 패키지를 관리할 권한이 있는 사용자를 지정할 수 있습니다.

+ R 및 Python 세션 서버가 계속 외부 스크립트에 문제가 발생 하는 경우에 정상적으로 실행 되도록 하는 별도 프로세스에서 실행 됩니다.

+ SQL Server를 사용 하 여 리소스 거 버 넌 스를 사용 하면 메모리 및 대규모 계산이 서버의 전반적인 성능을 저해 하지 않도록 외부 런타임 할당 된 프로세스를 제어할 수 있습니다.

관련된 태스크에 대 한 내용은 다음을 참조 하세요.
+ [기계 학습 솔루션 관리 및 모니터링](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>설계자와 데이터 엔지니어

설계자는 machine learning 수명 주기의 모든 측면에 걸쳐 있는 통합 된 워크플로 디자인 합니다. 데이터 엔지니어 디자인 ETL 솔루션을 빌드 및 machine learning 위해 기능 엔지니어링 작업을 최적화 하는 방법을 결정 합니다. 전체 데이터 플랫폼 경쟁 비즈니스 요구를 분산을 위해 설계 되어야 합니다.

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 비즈니스 인텔리전스, 데이터 웨어하우스 스택, 엔터프라이즈 클라우드 및 이동성 도구, Hadoop과 같은 다른 Microsoft 도구와 긴밀하게 통합되어 있기 때문에 고급 분석을 도모하려는 데이터 엔지니어나 시스템 설계자에게 다수의 이점을 제공합니다.

+ 데이터 집합 채우기, 그래픽, 생성 또는 예측을 구하려면 시스템 저장 프로시저를 사용 하 여 모든 Python 또는 R 스크립트를 호출 합니다. 없습니다 자세한 디자인에서 병렬 워크플로 데이터 과학 및 ETL 도구입니다. Azure Data Factory 및 Azure SQL Database에 대 한 지원을 쉽게 워크플로 학습 하는 컴퓨터에서 클라우드 데이터 원본을 사용 합니다.

+ 예약 및 machine learning 작업의 관리에 대 한 SQL server에서 Integration Services, SQL 에이전트, 또는 Azure Data Factory에 따라 표준 자동화 워크플로 사용 합니다. 또는 사용 하 여 합니다 [조작 화 기능](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r) Machine Learning Server에 있습니다.

관련된 태스크에 대 한 내용은 다음을 참조 하세요.

+ [SQL Server에서 기계 학습 워크플로에 만들기](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)

