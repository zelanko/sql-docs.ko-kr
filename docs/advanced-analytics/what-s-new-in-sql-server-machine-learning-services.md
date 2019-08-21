---
title: 새로운 기능
description: SQL Server 2016 R Services, R Server SQL Server Machine Learning Services의 각 릴리스에 대 한 새로운 기능 공지.
ms.date: 08/21/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f582088359c2878f5dfd84d4b353b1f9d8c369e5
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652298"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 새로운 기능

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

데이터 플랫폼, 고급 분석 및 데이터 과학 간의 통합을 계속 확장 하 고 확장 하 고 활용 하기 때문에 각 릴리스에서 SQL Server에 대 한 기계 학습 기능이 추가 되었습니다. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019-preview"></a>SQL Server 2019 미리 보기의 새로운

이 릴리스에는 SQL Server에서 R 및 Python machine learning 작업에 대 한 상위 요청 된 기능이 추가 되었습니다. 이 릴리스의 모든 기능에 대 한 자세한 내용은 [SQL Server 2019의 새로운](../sql-server/what-s-new-in-sql-server-ver15.md) 기능 및 [SQL Server 2019의 릴리스 정보](../sql-server/sql-server-ver15-release-notes.md)를 참조 하세요.

> [!NOTE]
> SQL Server 2019의 Java에 대 한 새로운 기능 설명서는 [SQL Server 언어 확장의 새로운 기능](https://docs.microsoft.com/sql/language-extensions/language-extensions-whats-new) 을 참조 하세요.

| 릴리스 | 기능 업데이트 |
|---------|----------------|
| RC 1 | [Python 또는 R 스크립트에서 SQL Server에 대 한 루프백 연결은](connect/loopback-connection.md) 이제 Windows 및 Linux 모두에서 지원 됩니다. |
| CTP 3.2 | 변경 내용이 없습니다. |
| CTP 3.1 | 변경 내용이 없습니다. |
| CTP 3.0 | 변경 내용이 없습니다. |
| CTP 2.5 | 변경 내용이 없습니다. |
| CTP 2.4 | R 및 Python에 대 한 Linux의 [CREATE EXTERNAL LIBRARY (transact-sql)](../t-sql/statements/create-external-library-transact-sql.md) 지원입니다. |
| CTP 2.3 | Windows 에서만 [CREATE EXTERNAL library (transact-sql)](../t-sql/statements/create-external-library-transact-sql.md) 문을 사용 하 여 외부 라이브러리에서 Python 코드에 액세스할 수 있습니다. |
| CTP 2.2 | 변경 내용이 없습니다. |
| CTP 2.1 | 변경 내용이 없습니다. |
| CTP 2.0 | R 및 Python machine learning에 대 한 Linux 플랫폼 지원. [Linux에서 SQL Server Machine Learning Services 설치](../linux/sql-server-linux-setup-machine-learning.md)를 시작 합니다. |
|  | [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 에는 분할 된 데이터에서 여러 모델을 쉽게 생성할 수 있는 두 개의 새 매개 변수가 도입 되었습니다. 이 자습서에서는 [R에서 파티션 기반 모델 만들기](tutorials/r-tutorial-create-models-per-partition.md)에 대해 자세히 알아보세요. |
|   | 이제 Windows 및 Linux에서 장애 조치 (Failover) 클러스터 지원이 지원 됩니다 .이는 모든 노드에서 SQL Server 실행 패드 서비스가 시작 된 것으로 가정 합니다. 자세한 내용은 [SQL Server 장애 조치 (failover) 클러스터 설치](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)를 참조 하세요. |

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>SQL Server 2017의 새로운

이 릴리스는 [Python 지원 및 업계 최고의 기계 학습 알고리즘](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)을 추가 합니다. 새 범위가 반영 되도록 이름이 바뀐 SQL Server 2017는 Python 및 R에 대 한 언어 지원과 함께 [SQL Server Machine Learning Services (데이터베이스 내)](what-is-sql-server-machine-learning.md)의 도입을 표시 합니다. 

기능 공지에 대 한 자세한 내용은 [SQL Server 2017의 새로운](../sql-server/what-s-new-in-sql-server-2017.md)기능을 참조 하세요.

### <a name="r-enhancements"></a>R 향상 된 기능

SQL Server Machine Learning Services의 R 구성 요소는 업데이트 된 버전의 기본 R, RevoScaler 및 기타 패키지를 포함 하는 차세대 SQL Server 2016 R Services입니다.

R의 새로운 기능에는 다음과 같은 주요 기능을 제공 하는 [**패키지 관리가**](r/install-additional-r-packages-on-sql-server.md)포함 되어 있습니다. 

+ 데이터베이스 역할은 Dba가 패키지를 관리 하 고 패키지 설치 권한을 할당 하는 데 도움이 됩니다.
+ [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 는 dba가 익숙한 t-sql 언어로 패키지를 관리 하는 데 도움이 됩니다.
+ [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) 함수를 통해 사용자가 소유 하는 패키지를 설치, 제거 또는 나열할 수 있습니다. 자세한 내용은 [RevoScaleR 함수를 사용 하 여 SQL Server에서 R 패키지를 찾거나 설치 하는 방법](r/use-revoscaler-to-manage-r-packages.md)을 참조 하세요.

### <a name="r-libraries"></a>R 라이브러리

| 패키지 | 설명 |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | 이 릴리스에서 MicrosoftML는 기본 R 설치에 포함 되어 있으므로 이전 SQL Server 2016 R 서비스에 필요한 업그레이드 단계를 제거 합니다. MicrosoftML는 원격 계산 컨텍스트에서 크기를 조정 하거나 실행할 수 있는 최신 기계 학습 알고리즘 및 데이터 변환을 제공 합니다. 알고리즘에는 사용자 지정 가능한 심층 신경망, 빠른 의사 결정 트리 및 의사 결정 포리스트, 선형 회귀, 로지스틱 회귀 등이 포함 됩니다.  |

### <a name="python-integration-for-in-database-analytics"></a>데이터베이스 내 분석을 위한 Python 통합

Python은 다양 한 기계 학습 작업을 위한 뛰어난 유연성과 강력한 기능을 제공 하는 언어입니다. Python 용 오픈 소스 라이브러리에는 사용자 지정 가능한 신경망을 위한 여러 플랫폼과 자연어 처리를 위한 인기 있는 라이브러리가 포함 되어 있습니다. 

Python은 데이터베이스 엔진과 통합 되기 때문에 데이터에 가까운 분석을 유지 하 고 데이터 이동과 관련 된 비용 및 보안 위험을 없앨 수 있습니다. Visual Studio와 같은 도구를 사용 하 여 Python을 기반으로 기계 학습 솔루션을 배포할 수 있습니다. 프로덕션 응용 프로그램에서는 SQL Server 데이터 액세스 방법을 사용 하 여 Python 3.5 런타임에서 예측, 모델 또는 시각적 개체를 가져올 수 있습니다.

T-sql 및 Python 통합은 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 시스템 저장 프로시저를 통해 지원 됩니다. 이 저장 프로시저를 사용 하 여 모든 Python 코드를 호출할 수 있습니다. 코드는 간단한 저장 프로시저를 사용 하 여 응용 프로그램에서 호출할 수 있는 Python 모델 및 스크립트의 엔터프라이즈급 배포를 가능 하 게 하는 안전한 이중 아키텍처로 실행 됩니다. SQL에서 Python 프로세스 및 MPI 링 병렬화의 데이터를 스트리밍하 여 추가 성능 향상을 얻을 수 있습니다.

T-sql [PREDICT](../t-sql/queries/predict-transact-sql.md) 함수를 사용 하 여 이전에 필요한 이진 형식으로 저장 된 미리 학습 된 모델에서 [기본 점수 매기기](sql-native-scoring.md) 를 수행할 수 있습니다.

### <a name="python-libraries"></a>Python 라이브러리

| 패키지 | 설명 |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| Python-RevoScaleR와 동일 합니다. 선형 및 로지스틱 회귀, 의사 결정 트리, 승격 된 트리 및 임의 포리스트, 모든 병렬화에 대 한 Python 모델을 만들어 원격 계산 컨텍스트에서 실행할 수 있습니다. 이 패키지는 여러 데이터 원본 및 원격 계산 컨텍스트를 사용할 수 있도록 지원 합니다. 데이터 과학자 또는 개발자는 원격 SQL Server에서 Python 코드를 실행 하 여 데이터를 이동 하지 않고 데이터를 탐색 하거나 모델을 만들 수 있습니다. |
|[**microsoftml**](python/ref-py-microsoftml.md) |Python-MicrosoftML R 패키지와 동일 합니다. |

### <a name="pre-trained-models"></a>미리 학습된 모델

Python과 R 모두에 [**미리 학습 된 모델**](install/sql-pretrained-models-install.md) 을 사용할 수 있습니다. 이미지 인식 및 긍정 부정 감정 분석을 위해 이러한 모델을 사용 하 여 사용자 고유의 데이터에 대 한 예측을 생성할 수 있습니다. 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>SQL Server 설치에서 공유 기능으로 서의 독립 실행형 서버

이 릴리스는 R 및 Python에서 통계 및 예측 분석을 지원 하 고 완전히 독립적인 데이터 과학 서버를 [SQL Server Machine Learning Server (독립 실행형)](r/r-server-standalone.md)도 추가 합니다. R Services와 마찬가지로이 서버는 SQL Server 2016 R Server (독립 실행형)의 다음 버전입니다. 독립 실행형 서버를 사용 하 여 SQL Server에 대 한 종속성 없이 R 또는 Python 솔루션을 배포 하 고 확장할 수 있습니다.
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2016"></a>SQL Server 2016의 새로운

이 릴리스에는 데이터베이스 엔진 인스턴스 내의 상주 데이터에서 R 스크립트를 처리 하기 위한 데이터베이스 내 분석 엔진인 **SQL Server 2016 R Services**를 통해 SQL Server에 대 한 기계 학습 기능이 도입 되었습니다.

또한 **SQL Server 2016 r server (독립 실행형)** 가 Windows 서버에 r server를 설치 하는 방법으로 출시 되었습니다. 처음에는 Windows 용 R Server를 설치 하는 유일한 방법이 제공 SQL Server 설치 프로그램이 제공 됩니다. 이후 릴리스에서 Windows에서 R Server를 원하는 개발자 및 데이터 과학자 다른 독립 실행형 설치 관리자를 사용 하 여 동일한 목표를 달성할 수 있습니다. SQL Server 독립 실행형 서버는 [Windows 용](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)독립 실행형 서버 제품 Microsoft R Server와 기능적으로 동일 합니다.

기능 공지에 대 한 자세한 내용은 [SQL Server 2016의 새로운](../sql-server/what-s-new-in-sql-server-2016.md)기능을 참조 하세요.

| 릴리스 |기능 업데이트 |
|---------|----------------|
| CU 추가 | [**실시간 점수 매기기**](real-time-scoring.md) 는 네이티브 C++ 라이브러리를 사용 하 여 최적화 된 이진 형식으로 저장 된 모델을 읽은 다음 R 런타임을 호출할 필요 없이 예측을 생성 합니다. 이렇게 하면 점수 매기기 작업이 훨씬 더 빨라집니다. 실시간 점수 매기기를 사용 하 여 저장 프로시저를 실행 하거나 R 코드에서 실시간 점수 매기기를 수행할 수 있습니다. 인스턴스를 최신 릴리스로 [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]업그레이드 하는 경우에는 SQL Server 2016에 대 한 실시간 점수 매기기를 사용할 수도 있습니다. |
| 초기 릴리스 | [**데이터베이스 내 분석을 위한 R 통합**](r/sql-server-r-services.md). <br/><br/> T-sql에서 R 함수를 호출 하기 위한 r 패키지 및 그 반대의 경우도 마찬가지입니다. RevoScaleR 함수는 구성 요소 부분으로 데이터를 청크 하 고 분산 처리를 조정 및 관리 하며 결과를 집계 하 여 규모에 따라 R 분석을 제공 합니다. SQL Server 2016 R Services (데이터베이스 내)에서 RevoScaleR 엔진은 데이터베이스 엔진 인스턴스와 통합 되며 동일한 처리 컨텍스트에서 데이터와 분석을 함께 brining 합니다. <br/><br/>[Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)를 통한 T-sql 및 R 통합. 이 저장 프로시저를 사용 하 여 모든 R 코드를 호출할 수 있습니다. 이 보안 인프라를 사용 하면 간단한 저장 프로시저를 사용 하 여 응용 프로그램에서 호출할 수 있는 모델 및 스크립트의 엔터프라이즈급 배포를 수행할 수 있습니다. SQL에서 R 프로세스 및 MPI 링 병렬화의 데이터를 스트리밍하 여 추가 성능 향상을 얻을 수 있습니다. <br/><br/>T-sql [PREDICT](../t-sql/queries/predict-transact-sql.md) 함수를 사용 하 여 이전에 필요한 이진 형식으로 저장 된 미리 학습 된 모델에서 [기본 점수 매기기](sql-native-scoring.md) 를 수행할 수 있습니다.|

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="linux-support"></a>Linux 지원

SQL Server 2019는 데이터베이스 엔진 인스턴스를 사용 하 여 기계 학습 패키지를 설치할 때 R 및 Python에 대 한 Linux 지원을 추가 합니다. 자세한 내용은 [Linux에서 SQL Server Machine Learning Services 설치](../linux/sql-server-linux-setup-machine-learning.md)를 참조 하세요.

Linux에서 SQL Server 2017에는 R 또는 Python 통합이 없지만, linux에서 실행 되는 T-sql [PREDICT](../t-sql/queries/predict-transact-sql.md)를 통해 해당 기능을 사용할 수 있기 때문에 Linux에서 [기본 점수 매기기](sql-native-scoring.md) 를 사용할 수 있습니다. 네이티브 점수 매기기를 사용 하 여 사전 학습 된 모델의 고성능 점수 매기기를 사용 하거나 R 런타임을 호출 하지 않아도 됩니다.
::: moniker-end

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>Azure SQL Database Machine Learning Services

Azure SQL Database의 Machine Learning Services는 공개 미리 보기로 제공 됩니다. 자세한 내용은 [Azure SQL Database Machine Learning Services (미리 보기)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview)를 참조 하세요.

## <a name="next-steps"></a>다음 단계

+ [Machine Learning Services SQL Server 설치 (데이터베이스 내)](install/sql-machine-learning-services-windows-install.md)
+ [Machine learning 자습서 및 샘플](tutorials/machine-learning-services-tutorials.md)
