---
title: 새로운 기능-SQL Server Machine Learning Services | Microsoft Docs
description: 새로운 기능 발표의 각 릴리스에 대 한 SQL Server 2016 R Services, R Server, SQL Server 2017의 Machine Learning Services.
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7c5871c6e33947f744dde571c329e8025b4a0813
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993443"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 새로운 기능

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

기계 학습 기능 계속 확장 하 고, 확장 및 데이터 플랫폼, 고급 분석 및 데이터 과학 간의 통합 향상 시킬 수에 따라 각 릴리스에서 SQL Server에 추가 됩니다. 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019-preview"></a>SQL Server 2019 preview의 새로운 기능

이 릴리스는 SQL Server에서 R 및 Python machine learning 작업에 대 한 상위 요청한 기능을 추가합니다. 모든이 릴리스의 기능에에서 대 한 자세한 내용은 참조 하세요. [What's New in SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) 하 고 [Release Notes for SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md)합니다.

> [!NOTE]
> 새로운 SQL Server 2019의 Java에 대 한 새 설명서를 참조 합니다 [SQL 서버 언어 확장의 새로운 기능?](https://docs.microsoft.com/sql/language-extensions/language-extensions-whats-new)

| 릴리스 | 기능 업데이트 |
|---------|----------------|
| CTP 2.5 | 변경 내용이 없습니다. |
| CTP 2.4 | 에 대 한 Linux 지원을 [CREATE EXTERNAL LIBRARY (TRANSACT-SQL)](../t-sql/statements/create-external-library-transact-sql.md) R 및 Python에 대 한 합니다. |
| CTP 2.3 | Windows에만 해당에서 Python 코드에서 액세스할 수 있습니다는 외부 라이브러리를 사용 하는 [CREATE EXTERNAL LIBRARY (TRANSACT-SQL)](../t-sql/statements/create-external-library-transact-sql.md) 문. |
| CTP 2.2 | 변경 내용이 없습니다. |
| CTP 2.1 | 변경 내용이 없습니다. |
| CTP 2.0 | R 및 Python machine learning 위해 Linux 플랫폼 지원 합니다. 시작 [설치할 SQL Server Machine Learning Services linux](../linux/sql-server-linux-setup-machine-learning.md)합니다. |
|  | 합니다 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 쉽게 분할 된 데이터에서 여러 모델을 생성할 수 있도록 하는 두 개의 새 매개 변수를 소개 합니다. 이 자습서에서 자세히 알아보세요 [R에서 모델 파티션 만들기](tutorials/r-tutorial-create-models-per-partition.md)합니다. |
|   | 장애 조치 클러스터 지원 Windows 및 Linux, SQL Server 실행 패드 서비스가 모든 노드에서 시작 하는 것으로 가정에서 이제 지원 됩니다. 자세한 내용은 [SQL Server 장애 조치 클러스터 설치](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)합니다. |

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>SQL Server 2017의에서 새로운 기능

이 릴리스에 추가 되었습니다 [Python 지원 및 업계 최고의 기계 학습 알고리즘](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)합니다. 새 범위를 반영 하도록 이름이 바뀌었거나, SQL Server 2017 표시 미치는 [SQL Server Machine Learning Services (In-database)](what-is-sql-server-machine-learning.md), Python 및 R 모두에 대 한 언어 지원 

상향 기능 공지 사항 모두에 대 한 참조 [What's New in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)합니다.

### <a name="r-enhancements"></a>R의 향상 된 기능

SQL Server 2017의 Machine Learning Services의 R 구성 요소는 기본 R, RevoScaler 및 기타 패키지의 업데이트 된 버전을 사용 하 여 SQL Server 2016 R Services의 다음 세대입니다.

R에 대 한 새 기능에 포함 됩니다 [ **패키지 관리**](r/install-additional-r-packages-on-sql-server.md)를 다음 강조 표시를 사용 하 여: 

+ 데이터베이스 역할에는 패키지를 관리 하 고 패키지 설치에 대 한 권한을 할당 하는 Dba 데 도움이 됩니다.
+ [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 친숙 한 T-SQL 언어 패키지를 관리 하는 Dba 하도록 도와줍니다.
+ [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) 함수 설치, 제거 또는 목록 패키지 사용자가 소유 하는 데 도움이 됩니다. 자세한 내용은 [SQL Server에서 R을 설치 하거나 RevoScaleR 함수를 사용 하는 방법을 패키지](r/use-revoscaler-to-manage-r-packages.md)합니다.

### <a name="r-libraries"></a>R 라이브러리

| 패키지 | Description |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | 이 릴리스에서 MicrosoftML 이전 SQL Server 2016 R Services에 필요한 업그레이드 단계를 제거는 기본 R 설치에 포함 됩니다. MicrosoftML의 최첨단 기계 학습 알고리즘 및 크기를 조정 하거나 원격 계산 컨텍스트에서 실행할 수 있는 데이터 변환을 제공 합니다. 사용자 지정 가능한 심층 신경망, 빠른 의사 결정 트리 및 의사 결정 포리스트, 선형 회귀 및 로지스틱 회귀 알고리즘에 포함 됩니다.  |

### <a name="python-integration-for-in-database-analytics"></a>데이터베이스 내 분석에 대 한 Python 통합

Python은 기계 학습 작업의 다양 한 기능과 뛰어난 유연성을 제공 하는 언어입니다. Python 용 오픈 소스 라이브러리는 사용자 지정 가능한 신경망에 대 한 여러 플랫폼 및 자연어 처리를 위한 인기 있는 라이브러리를 포함합니다. 이제이 널리 사용 되는 언어는 SQL Server 2017의 Machine Learning에서 지원 됩니다.

Python과 데이터베이스 엔진을 사용 하 여 통합 데이터에 근접 한 분석을 유지할 수 있으며 비용 및 데이터 이동과 관련 된 보안 위험을 제거할 수 있습니다. Visual Studio와 같은 도구를 사용 하 여 Python을 기반으로 기계 학습 솔루션을 배포할 수 있습니다. 프로덕션 응용 프로그램에 예측 모델을 가져올 수 있습니다 또는 시각적 개체에서 SQL Server 데이터를 사용 하 여 Python 3.5 런타임 메서드에 액세스 합니다.

통해 T-SQL 및 Python 통합은 지원 합니다 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 시스템 저장 프로시저입니다. 이 저장된 프로시저를 사용 하 여 모든 Python 코드를 호출할 수 있습니다. 엔터프라이즈급 배포 Python 모델 및 스크립트와 간단한 저장된 프로시저를 사용 하 여 응용 프로그램에서 호출할 수 있도록 안전 하 고 이중 아키텍처에서 코드가 실행 됩니다. SQL에서 Python 프로세스 및 MPI 링 병렬화로 스트리밍 데이터에서 추가 성능 향상.

T-SQL을 사용할 수 있습니다 [PREDICT](../t-sql/queries/predict-transact-sql.md) 수행 하는 함수 [네이티브 점수 매기기](sql-native-scoring.md) 필요한 이진 형식으로 이전에 저장 하는 미리 학습 된 모델입니다.

### <a name="python-libraries"></a>Python 라이브러리

| 패키지 | Description |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| Python-RevoScaleR에 해당 합니다. 선형 및 로지스틱 회귀, 의사 결정 트리, 승격 된 트리 및 임의 포리스트의 모든 병렬 및 원격 계산 컨텍스트에서 실행 되 고 수에 대 한 Python 모델을 만들 수 있습니다. 이 패키지는 여러 데이터 원본 및 원격 계산 컨텍스트 사용을 지원합니다. 데이터 과학자 또는 개발자가 데이터를 탐색 하거나 데이터를 이동 하지 않고 모델을 작성 하는 원격 SQL Server에서 Python 코드를 실행할 수 있습니다. |
|[**microsoftml**](python/ref-py-microsoftml.md) |MicrosoftML R 패키지의 Python에 해당 합니다. |

### <a name="pre-trained-models"></a>미리 학습된 모델

[**미리 학습 된 모델** ](install/sql-pretrained-models-install.md) Python 및 R 모두를 사용 하 여 이러한 모델은 이미지 인식과 긍정 음수가 감성 분석, 사용자 고유의 데이터에서 예측을 생성할 수 있습니다. 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>SQL Server 설치 프로그램에서 공유 기능으로 독립 실행형 서버

이 릴리스는 또한 추가 [SQL Server Machine Learning Server (독립 실행형)](r/r-server-standalone.md), R 및 Python에서 통계 및 예측 분석을 지 원하는, 완전히 독립적인 데이터 과학 서버. 로이 서버는 R Services를 사용 하 여 다음 버전의 SQL Server 2016 R Server (독립 실행형). 독립 실행형 서버를 사용 하 여 배포 및 SQL Server에 종속성이 없는 R 또는 Python 솔루션을 확장할 수 있습니다.
::: moniker-end

## <a name="new-in-sql-server-2016"></a>SQL Server 2016의에서 새로운 기능

이 릴리스에 도입 된 기계 학습을 통해 SQL server 기능 **SQL Server 2016 R Services**, 데이터베이스 엔진 인스턴스를 내 상주 데이터에 대해 처리 R 스크립트에 대 한 데이터베이스 내 분석 엔진입니다.

또한 **SQL Server 2016 R Server (독립 실행형)** Windows 서버에서 R Server를 설치 하는 방법으로 릴리스 되었습니다. 처음에 SQL Server 설치 프로그램에는 Windows에 대 한 R Server를 설치 하는 유일한 방법은 제공 합니다. 이후 릴리스에서 개발자 및 데이터 과학자의 R Server에 Windows 하고자 했던 동일한 목표를 달성 하려면 다른 독립 실행형 설치 관리자를 사용할 수 있습니다. SQL Server의 독립 실행형 서버는 독립 실행형 서버 제품에 기능적 [Microsoft R Server에 대 한 Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)합니다.

상향 기능 공지 사항 모두에 대 한 참조 [What's New in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)합니다.

| 릴리스 |기능 업데이트 |
|---------|----------------|
| CU 추가 | [**실시간 점수 매기기** ](real-time-scoring.md) 네이티브 의존 C++ 라이브러리를 최적화 된 이진 형식으로 저장 된 모델을 읽고 다음 R 런타임을 호출 하지 않고 예측을 생성 합니다. 이렇게 하면 점수 매기기 작업을 훨씬 더 빠릅니다. 실시간 점수 매기기를 사용 하 여 저장된 프로시저를 실행할 수도 있고 R 코드에서 실시간 점수 매기기를 수행할 수 있습니다. 실시간 점수 매기기 역시 사용할 수 있는 SQL Server 2016에 대 한 인스턴스를 최신 릴리스로 업그레이드 되 면 [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]합니다. |
| 초기 릴리스 | [**데이터베이스 내 분석에 R 통합**](r/sql-server-r-services.md)합니다. <br/><br/> 호출 R에 대 한 R 패키지에는 t-sql로 또는 그 반대로 작동 합니다. 관리 분산 처리 및 결과 집계 및 RevoScaleR 함수 조정 구성 요소로 데이터를 청크 하 여 대규모 R 분석을 제공 합니다. SQL Server 2016 R Services (In-database)에서 RevoScaleR 엔진 데이터 및 분석 같은 처리 컨텍스트에서 함께 brining 데이터베이스 엔진 인스턴스를 통합 되어 있습니다. <br/><br/>T-SQL 및 R 통합을 통해 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)합니다. 이 저장된 프로시저를 사용 하 여 R 코드를 호출할 수 있습니다. 이 보안 인프라에 보냈습니다 모델 및 간단한 저장된 프로시저를 사용 하 여 응용 프로그램에서 호출할 수 있는 스크립트의 엔터프라이즈급 배포할을 수 있습니다. SQL에서 R 프로세스 및 MPI 링 병렬화로 스트리밍 데이터에서 추가 성능 향상. <br/><br/>T-SQL을 사용할 수 있습니다 [PREDICT](../t-sql/queries/predict-transact-sql.md) 수행 하는 함수 [네이티브 점수 매기기](sql-native-scoring.md) 필요한 이진 형식으로 이전에 저장 하는 미리 학습 된 모델입니다.|

## <a name="linux-support-roadmap"></a>Linux 지원 로드맵

SQL Server 2019 CTP 2.3 기계 학습 데이터베이스 엔진 인스턴스를 사용 하 여 패키지를 설치할 때 R 및 Python에 대 한 Linux 지원을 추가 합니다. 자세한 내용은 [설치할 SQL Server Machine Learning Services linux](../linux/sql-server-linux-setup-machine-learning.md)합니다.

Linux에서 SQL Server 2017는 R 또는 Python 통합 없지만 사용할 수 있습니다 [네이티브 점수 매기기](sql-native-scoring.md) Linux에서 해당 기능을 T-SQL을 통해 사용할 수 있으므로 [PREDICT](../t-sql/queries/predict-transact-sql.md), Linux에서 실행 되는 합니다. 네이티브 점수 매기기를 호출 하거나 심지어는 R 런타임 요구 하지 않고 미리 학습 된 모델에서 점수 매기기 고성능 수 있습니다.

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>Machine Learning에서 Azure SQL Database 서비스

Machine Learning 서비스 (R)을 사용한 Azure SQL Database의 공개 미리 보기로 제공 됩니다. 자세한 내용은 [R (미리 보기)를 사용 하 여 Azure SQL Database Machine Learning Services](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview)합니다.

## <a name="next-steps"></a>다음 단계

+ [SQL Server 2017 Machine Learning Services (In-database) 설치](install/sql-machine-learning-services-windows-install.md)
+ [Machine learning 자습서 및 샘플](tutorials/machine-learning-services-tutorials.md)
