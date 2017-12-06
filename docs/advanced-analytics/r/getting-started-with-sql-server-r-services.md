---
title: "SQL Server 시작 기계 학습 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 12/07/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: "34"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6f211088484178e652cd7ea489490b5654ef50d8
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="getting-started-with-sql-server-machine-learning"></a>SQL Server 시작 기계 학습

SQL Server의 컴퓨터 학습 서비스 보안 위험이 나 데이터 unnecesarily 이동 하 여 데이터를 노출 하지 않고 데이터 과학 작업을 지원 하도록 설계 되었습니다.

+ SQL Server 2016에서 선호 하는 R 도구를 사용 하지만 동시에 성능 수십 억 개의 레코드를 분석을 확장 수 있습니다. 기계 학습을 SQL Server와 통합 다시 코딩 하지 않고도 R 코드를 두 프로덕션 환경에 수는 또한 의미 합니다.

+ SQL Server 2017 동일한 확장 프레임 워크를 사용 하 여 Python 코드에 대 한 지원을 추가 합니다.

이 항목 R 또는 Python에-데이터베이스를 사용 하기 위한 주요 시나리오에 설명 하 고 솔루션 시작 수 있도록 리소스를 제공 합니다.

적용 대상: SQL Server 2016 R Services, SQL Server 2017 기계 학습 Services (In-database)

> [!NOTE]
> SQL Server 2016에서는 R 언어에 대해서만 지원 합니다. Python 언어를 지원 하려면 SQL Server 2017 CTP 2.0 합니다.

## <a name="step-1-set-up-sql-server-machine-learning-services"></a>1단계. SQL Server 컴퓨터 학습 서비스 설정

1. SQL Server 설치 프로그램을 실행 하 고 SQL Server 데이터베이스 엔진의 하나 이상의 인스턴스를 설치 합니다.
2. 외부 런타임 실행을 지 원하는 기능을 추가 합니다.
3. SQL Server 2016 R는 기본적으로 추가 됩니다. SQL Server 2017 년에 추가 하려면 언어를 선택 해야 합니다. Python 또는 R 선택 하거나 둘 다 사용 수 있습니다.
4. 설치가 완료 되 면 외부 스크립트 실행을 사용 하도록 설정 하려면 몇 가지 추가 단계를 수행 하 고 서버를 다시 시작 합니다.

**리소스**

+ [SQL Server와 기계 학습 설정](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

> [!TIP]  
> R 작업용 서버는 만들어야 하지만 SQL Server는 필요하지 않나요? [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx)를 사용해 보세요.  

## <a name="step-2-develop-your-r-or-python-solutions"></a>2단계. R 또는 Python 솔루션 개발

데이터 과학자 일반적으로 사용 R, Python 자신의 랩톱 또는 개발 워크스테이션에서 데이터를 탐색 하 고 빌드 및는 좋은 예측 모델을 얻을 때까지 예측 모델을 조정 하려면. 

SQL Server의 컴퓨터 학습 서비스를이 프로세스를 변경할 필요가 없습니다 생깁니다. 설치가 완료 되 면에서 Python 또는 R 코드를 실행할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 또는 원격으로:

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **원하는 IDE를 사용 하 여**합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 클라이언트 구성 요소는 데이터 과학자의 실험 및 개발에 필요한 모든 도구를 제공합니다. 이러한 도구에는 R 런타임, 표준 R 작업의 성능을 향상시키기 위한 인텔 수학 커널 라이브러리 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R 코드 실행을 지원하는 향상된 R 패키지 집합이 포함됩니다.  

+ **원격 또는 로컬로 작업**합니다. 데이터 과학자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하여 평소와 같이 로컬 분석을 위해 클라이언트에 제공합니다. 그러나 더 나은 방법은 **ScaleR** API를 사용해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 계산을 푸시하여 비용이 많이 들고 안전하지 않은 데이터를 이동을 방지하는 것입니다.

+ **R, Python 스크립트를 포함 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저**합니다. 코드 최적화 완벽 하 게 될 때 불필요 한 데이터 이동을 방지 하 고 데이터 처리 작업을 최적화 하는 저장된 프로시저에서 래핑해야 합니다.


**리소스**

+ 설치 [R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation) 또는 RStudio 합니다.  

## <a name="step-3-optimize"></a>3단계. 최적화

모델 크기를 조정할 엔터프라이즈 데이터 준비 되 면 데이터 과학자와 같은 프로세스를 최적화 하기 위해 DBA 또는 SQL 개발자 작업 종종 됩니다.

+ 기능 엔지니어링
+ 데이터 수집 및 데이터 변환
+ 점수 매기기

일반적으로 R을 사용 하는 데이터 과학자 특히 큰 데이터 집합을 사용 하는 경우에 성능 및 확장성을 모두 문제가 했습니다. 공용 런타임 구현이 단일 스레드 이며 로컬 컴퓨터에서 사용할 수 있는 메모리 데이터 집합만 수용할 수 때문입니다. SQl Server 컴퓨터 학습 서비스와의 통합 더 많은 데이터와 함께 성능 향상을 위해 여러 기능을 제공합니다.

+ **RevoScaleR**.:이 R 패키지에 일부 병렬 처리 및 확장성을 제공 하도록 다시 설계 하는 가장 인기 있는 R 함수를 구현 합니다. 또한 일반적으로는 훨씬 큰 메모리와 계산력을 갖춘 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 계산을 푸시하여 성능과 확장을 더 증대하는 함수도 포함되어 있습니다.

+ **revoscalepy**합니다. 분산 처리를 지 원하는 대부분의 알고리즘을이 Python 라이브러리를 새로 추가 되거나 SQL Server 2017 CTP 2.0 에서만 사용할 수 RevoScaleR의 원격 계산 컨텍스트 등 가장 인기 있는 기능을 구현.

+ 작업에 대 한 적합 한 언어를 선택 합니다.  R은 SQL을 사용 하 여 구현 하기 어려운 통계적 계산에 가장 적합 합니다. 데이터에 대해 집합 기반 작업에 대 한 성능을 활용해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 최대 성능을 얻을 수 있도록 합니다. 열에 대해 매우 빠른 계산을 위한 메모리 내 데이터베이스 엔진을 사용 합니다.

**리소스**

+ [성능 사례 연구](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R 및 데이터 최적화](../../advanced-analytics/r/r-and-data-optimization-r-services.md)


## <a name="step-4-deploy-and-consume"></a>4단계. 배포 및 사용

R 스크립트 또는 모델이 프로덕션 환경에서 사용할 준비가 되 면 응용 프로그램에서 저장된 된 R, Python 코드를 호출할 수 있도록 데이터베이스 개발자는 저장된 프로시저에 코드 또는 모델 포함 될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 R 코드를 저장하고 실행하면 많은 이점이 있습니다. 편리한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 인터페이스를 사용하고 모든 계산이 데이터베이스에서 실행되어 불필요한 데이터 이동을 방지할 수 있습니다.

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **안전 하 고 확장 가능한**합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 는 데이터베이스 엔진의 보안을 유지하고 R 세션을 격리하는 새로운 확장성 아키텍처를 사용합니다. 또한, R 스크립트를 실행할 수 있는 사용자를 제어하고 R 코드로 액세스할 수 있는 데이터베이스를 지정할 수도 있습니다. 대규모 계산이 서버의 전반적인 성능을 저해하지 않도록 R 런타임에 할당된 리소스 양을 제어할 수 있습니다.

+ **일정 예약 및 감사**합니다. 외부 스크립트 작업 실행 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 제어할 수 있습니다 및 감사 데이터는 데이터 과학자 사용 합니다. 작업 및 T-SQL 작업 또는 저장된 프로시저를 예약 하는 것 처럼 외부 Python 또는 R 스크립트를 포함 하는 워크플로 작성 예약할 수 있습니다.

활용 되는 리소스 관리 및 보안 기능에 SQL Server를 배포 프로세스에는 이러한 작업 포함 될 수 있습니다.

+ 저장된 프로시저에서 최적으로 실행할 수 있는 함수에 R 코드 변환
+ 보안을 설정 하 고 특정 작업에 의해 사용 되는 패키지를 잠그는
+ 리소스 관리를 사용 하도록 설정

**리소스**

+ [R에 대 한 리소스 관리](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [SQL Server에 대 한 R 패키지 관리](../../advanced-analytics/r/r-package-management-for-sql-server-r-services.md)

## <a name="quick-starts"></a>빠른 시작

이 연습에서 데이터 모델 만들기 및 SQL Server로 배포를 탐색 하는 전체 워크플로 이해을 읽습니다.

+ [데이터 과학 종단 간 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

확장 가능 하며 높은 성능 분석을 위해 RevoScaleR 패키지를 사용 하는 방법을 알아봅니다.

+ [데이터 과학 심층 분석: RevoScaleR 패키지 사용](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

데이터 개발자를 위해 특별히 모든 R 코드가 제공! SQL 저장 프로시저를 만들거나 모델을 학습에 R을 포함 하 고 저장 된 모델에서 예측을 확보 하는 방법에 알아봅니다.

+ [SQL 개발자를 위한 데이터베이스 내 고급 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

저장된 프로시저에서 호출 R에 대 한 구문에 알아봅니다.

+ [Transact-SQL에서 R 코드 사용](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

## <a name="solutions"></a>솔루션

자세한 예제에 대 한 업계 비롯 하 여 = 특정 솔루션 템플릿을 참조 [SQL Server 컴퓨터 학습 자습서](../tutorials/machine-learning-services-tutorials.md)합니다.
