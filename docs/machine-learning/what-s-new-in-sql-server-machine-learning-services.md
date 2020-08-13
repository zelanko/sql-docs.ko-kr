---
title: SQL Server Machine Learning Services의 새로운 기능
titleSuffix: ''
description: SQL Server Machine Learning Services 및 SQL Server 2016 R Services의 각 릴리스에 대한 새로운 기능 알림입니다.
ms.date: 11/04/2019
ms.topic: overview
author: dphansen
ms.author: davidph
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning-services
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7e4092bd98749006b6f68b8c55fee3baca678255
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245262"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 새로운 기능

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

Microsoft는 데이터 플랫폼, 고급 분석 및 데이터 과학 간의 통합을 계속 확장하고 발전시키고 있으며, 릴리스마다 SQL Server에 기계 학습 기능을 추가하고 있습니다. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019"></a>SQL Server 2019의 새로운 기능

이 릴리스에는 SQL Server에서 Python 및 R 기계 학습 작업에 대해 가장 많이 요청된 기능이 추가되었습니다. 이 릴리스의 모든 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md) 및 [Release Notes for SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md)(SQL Server 2019 릴리스 정보)를 참조하세요.

> [!NOTE]
> SQL Server 2019의 Java에 대한 새로운 기능 설명서는 [SQL Server 언어 확장의 새로운 기능](https://docs.microsoft.com/sql/language-extensions/language-extensions-whats-new)을 참조하세요.

다음은 **Windows** 및 **Linux** 모두에서 사용할 수 있는 SQL Server Machine Learning Services의 새로운 기능입니다.

- Linux 플랫폼 지원은 Python 및 R용 Machine Learning Services에 추가되었습니다. [Linux에서 SQL Server Machine Learning Services 설치](../linux/sql-server-linux-setup-machine-learning.md)를 시작하세요.
- [Python 또는 R 스크립트에서 SQL Server에 루프백 연결](connect/loopback-connection.md). 
- Python 및 R용 [CREATE EXTERNAL LIBRARY(Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md).
- [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)에는 분할된 데이터로 여러 모델을 쉽게 생성할 수 있는 두 개의 새 매개 변수가 도입되었습니다. [R에서 파티션 기반 모델 만들기](tutorials/r-tutorial-create-models-per-partition.md) 자습서에서 자세한 내용을 알아보세요.
- 장애 조치(failover) 클러스터 지원은 실행 패드 서비스에 사용할 수 있습니다(모든 노드에서 SQL Server 실행 패드 서비스가 시작된 것으로 가정). 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터 설치](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)를 참조하세요.
- Machine Learning Services에 대한 격리 메커니즘 변경 내용. 자세한 내용은 [Windows의 SQL Server 2019: Machine Learning Services에 대한 격리 변경 내용의 파일 사용 권한 섹션](install/sql-server-machine-learning-services-2019.md)을 참조하세요.

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>SQL Server 2017의 새로운 기능

이 릴리스에는 [Python 지원 및 업계 최고 수준의 기계 학습 알고리즘](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)이 추가되었습니다. 새로운 범위를 반영하도록 이름이 바뀐 SQL Server 2017에는 Python 및 R 언어 지원과 함께 [SQL Server Machine Learning Services(데이터베이스 내)](sql-server-machine-learning-services.md)가 도입되었습니다. 

전체 기능 공지는 [SQL Server 2017의 새로운 기능](../sql-server/what-s-new-in-sql-server-2017.md)을 참조하세요.

### <a name="r-enhancements"></a>R 개선 사항

SQL Server Machine Learning Services의 R 구성 요소는 업데이트된 버전의 기본 R, RevoScaler 및 기타 패키지를 포함하는 차세대 SQL Server 2016 R Services입니다.

R의 새로운 기능으로 [**패키지 관리**](package-management/install-r-packages-with-tsql.md)가 있으며, 핵심 내용은 다음과 같습니다. 

+ 데이터베이스 역할은 DBA가 패키지를 관리하고 패키지 설치 권한을 할당하는 데 도움이 됩니다.
+ [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)는 DBA가 익숙한 T-SQL 언어로 패키지를 관리할 수 있게 도와줍니다.
+ [RevoScaleR](package-management/install-r-packages-with-revoscaler.md) 함수는 사용자 소유의 패키지를 설치, 제거 또는 나열할 수 있습니다. 자세한 내용은 [SQL Server에서 RevoScaleR 함수를 사용하여 R 패키지를 찾거나 설치하는 방법](package-management/install-r-packages-with-revoscaler.md)을 참조하세요.

### <a name="r-libraries"></a>R 라이브러리

| 패키지 | Description |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | 이 릴리스에서는 MicrosoftML이 기본 R 설치에 포함되어 있으므로, 이전 SQL Server 2016 R Services와는 달리 업그레이드 단계가 필요 없습니다. MicrosoftML은 원격 컴퓨팅 컨텍스트에서 크기를 조정하거나 실행할 수 있는 최신 기계 학습 알고리즘 및 데이터 변환을 제공합니다. 알고리즘으로는 사용자 지정 가능한 심층 신경망, 빠른 의사 결정 트리 및 의사 결정 포리스트, 선형 회귀, 로지스틱 회귀 등이 있습니다.  |

### <a name="python-integration-for-in-database-analytics"></a>데이터베이스 내 분석을 위한 Python 통합

Python은 다양한 기계 학습 작업을 위한 뛰어난 유연성과 강력한 기능을 제공하는 언어입니다. Python용 오픈 소스 라이브러리에는 사용자 지정 가능한 신경망을 위한 여러 플랫폼과 자연어 처리를 위한 인기 있는 라이브러리가 포함되어 있습니다. 

Python은 데이터베이스 엔진과 통합되므로, 데이터와 밀접하게 분석을 유지하고 데이터 이동과 연관된 비용 및 보안 위험을 제거할 수 있습니다. Visual Studio 같은 도구를 사용하여 Python을 기반으로 기계 학습 솔루션을 배포할 수 있습니다. 프로덕션 애플리케이션에서는 SQL Server 데이터 액세스 방법을 사용하여 Python 3.5 런타임에서 예측, 모델 또는 시각적 개체를 가져올 수 있습니다.

T-SQL과 Python의 통합은 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 시스템 저장 프로시저를 통해 지원됩니다. 이 저장 프로시저를 사용하여 모든 Python 코드를 호출할 수 있습니다. 코드는 간단한 저장 프로시저를 사용하여 애플리케이션에서 호출할 수 있는 Python 모델 및 스크립트의 엔터프라이즈급 배포를 지원하는 안전한 이중 아키텍처에서 실행됩니다. SQL에서 Python 프로세스로 데이터를 스트리밍하고 MPI 링 병렬화를 사용하여 성능을 추가로 향상할 수 있습니다.

T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) 함수를 사용하여 이전에 필수 이진 형식으로 저장된 미리 학습된 모델에 대한 [네이티브 채점](predictions/native-scoring-predict-transact-sql.md)을 수행할 수 있습니다.

### <a name="python-libraries"></a>Python 라이브러리

| 패키지 | Description |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| RevoScaleR과 동일한 Python 명령입니다. 모두 병렬화 가능하고 원격 컴퓨팅 컨텍스트에서 실행 가능한 선형 및 로지스틱 회귀, 의사 결정 트리, 승격된 트리 및 임의 포리스트에 대한 Python 모델을 만들 수 있습니다. 이 패키지는 여러 데이터 원본 및 원격 컴퓨팅 컨텍스트 사용을 지원합니다. 데이터 과학자 또는 개발자는 원격 SQL Server에서 Python 코드를 실행하여 데이터를 이동하지 않고도 데이터를 검색하거나 모델을 만들 수 있습니다. |
|[**microsoftml**](python/ref-py-microsoftml.md) |MicrosoftML R 패키지와 동일한 Python 명령입니다. |

### <a name="pre-trained-models"></a>미리 학습된 모델

[**미리 학습된 모델**](install/sql-pretrained-models-install.md)을 Python과 R에 모두 사용할 수 있습니다. 이러한 모델을 이미지 인식 및 긍정적-부정적 감정 분석에 사용하여 고유의 데이터에 대한 예측을 생성할 수 있습니다. 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>SQL Server 설치 프로그램의 공유 기능인 독립 실행형 서버

또한 이 릴리스에는 완전한 독립 데이터 과학 서버로써 R 및 Python에서 통계 및 예측 분석을 지원하는 [SQL Server Machine Learning Server(독립 실행형)](r/r-server-standalone.md)가 추가되었습니다. R Services와 마찬가지로, 이 서버는 SQL Server 2016 R Server(독립 실행형)의 다음 버전입니다. 독립 실행형 서버를 사용하면 SQL Server에 종속되지 않고 R 또는 Python 솔루션을 배포하고 확장할 수 있습니다.
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2016"></a>SQL Server 2016의 새로운 기능

이 릴리스에서는 데이터베이스 엔진 인스턴스 내의 상주 데이터에서 R 스크립트를 처리하기 위한 데이터베이스 내 분석 엔진인 **SQL Server 2016 R Services**를 통해 기계 학습 기능이 SQL Server에 도입되었습니다.

또한 Windows 서버에 R Server를 설치하는 방법으로 **SQL Server 2016 R Server(독립 실행형)** 가 출시되었습니다. 처음에는 Windows용 R Server를 설치하는 유일한 방법으로 SQL Server 설치 프로그램이 제공되었습니다. 이후 릴리스에서는 Windows에서 R Server를 원하는 개발자 및 데이터 과학자가 다른 독립 실행형 설치 관리자를 사용하여 동일한 목표를 달성할 수 있습니다. SQL Server의 독립 실행형 서버는 독립 실행형 서버 제품 [Windows용 Microsoft R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)와 기능적으로 동일합니다.

전체 기능 공지는 [SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)을 참조하세요.

| 해제 |기능 업데이트 |
|---------|----------------|
| CU 추가 | [**실시간 채점**](predictions/real-time-scoring.md)은 네이티브 C++ 라이브러리를 사용하여 최적의 이진 형식으로 저장된 모델을 읽은 다음, R 런타임을 호출할 필요 없이 예측을 생성합니다. 따라서 채점 작업이 훨씬 빨라집니다. 실시간 채점을 사용하면 R 코드에서 저장 프로시저를 실행하거나 실시간 채점을 수행할 수 있습니다. 인스턴스가 [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]의 최신 릴리스로 업그레이드된 경우에는 SQL Server 2016에도 실시간 채점을 사용할 수 있습니다. |
| 초기 릴리스 | [**데이터베이스 내 분석을 위한 R 통합**](r/sql-server-r-services.md) <br/><br/> T-SQL에서 R 함수를 호출하거나 그 반대로 호출하기 위한 R 패키지입니다. RevoScaleR 함수는 데이터를 구성 요소 부분으로 청크하고, 분산 처리를 조정 및 관리하고, 결과를 집계하여 규모에 따라 R 분석을 제공합니다. SQL Server 2016 R Services(데이터베이스 내)에서 RevoScaleR 엔진은 데이터베이스 엔진 인스턴스와 통합되어 데이터와 분석을 동일한 처리 컨텍스트로 가져옵니다. <br/><br/>[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)를 통해 T-SQL과 R 통합. 이 저장 프로시저를 사용하여 모든 R 코드를 호출할 수 있습니다. 이 보안 인프라는 간단한 저장 프로시저를 사용하여 애플리케이션에서 호출할 수 있는 R 모델 및 스크립트의 엔터프라이즈급 배포를 지원합니다. SQL에서 R 프로세스로 데이터를 스트리밍하고 MPI 링 병렬화를 사용하여 성능을 추가로 향상할 수 있습니다. <br/><br/>T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) 함수를 사용하여 이전에 필수 이진 형식으로 저장된 미리 학습된 모델에 대한 [네이티브 채점](predictions/native-scoring-predict-transact-sql.md)을 수행할 수 있습니다.|

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="linux-support"></a>Linux 지원

SQL Server 2019는 데이터베이스 엔진 인스턴스를 사용하여 기계 학습 패키지를 설치할 때 R 및 Python에 Linux를 사용할 수 있도록 지원이 추가되었습니다. 자세한 내용은 [Linux에 SQL Server Machine Learning Services 설치](../linux/sql-server-linux-setup-machine-learning.md)를 참조하세요.

Linux에서는 SQL Server 2017이 R 또는 Python과 통합되지 않지만, Linux에서 실행되는 T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md)를 통해 해당 기능을 사용할 수 있으므로 Linux에서 [네이티브 채점](predictions/native-scoring-predict-transact-sql.md)을 사용할 수 있습니다. 네이티브 채점을 사용하면 R 런타임을 호출하지 않고 또는 심지어 R 런타임 없이, 미리 학습된 모델에서 고성능 채점이 가능합니다.
::: moniker-end

## <a name="next-steps"></a>다음 단계

+ [SQL Server Machine Learning Services 설치(데이터베이스 내)](install/sql-machine-learning-services-windows-install.md)
