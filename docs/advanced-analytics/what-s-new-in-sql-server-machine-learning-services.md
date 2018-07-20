---
title: 새로운&#39;SQL Server Machine Learning Services의 새로운 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/02/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bf56d52823727609d713639d534e277be57caaef
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174810"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 새로운 기능 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

기계 학습 기능 계속 확장 하 고, 확장 및 데이터 플랫폼 및 분석, 데이터 과학 간의 통합 향상 시킬 수에 따라 각 릴리스에서 SQL Server에 추가 되 고 감독 학습 데이터에 대해 구현 하려는. 

## <a name="new-in-sql-server-2017"></a>SQL Server 2017의에서 새로운 기능

이 릴리스에서 Python 지원 및 업계 최고의 기계 학습 알고리즘을 추가 했습니다. 새 범위를 반영 하도록 이름이 바뀌었거나, SQL Server 2017 표시 미치는 **SQL Server Machine Learning Services (In-database)**, Python 및 R 모두에 대 한 언어 지원 

이 릴리스에 도입 **SQL Server Machine Learning Server (독립 실행형)** 전용된 시스템에서 실행 하려는 R 및 Python 워크 로드에 대 한 SQL Server의 완전히 독립적입니다. 독립 실행형 서버를 사용 하 여 배포 및 SQL Server를 사용 하지 않고 R 또는 Python 솔루션을 확장할 수 있습니다.

| 릴리스 | 기능 업데이트 |
|---------|----------------|
| CU 6 | 버그 수정 및 패키지 새로 고침 했지만 공지 새 기능입니다. 미리 학습 된 모델은 누락 된 경우 수정 날짜/시간 데이터 형식에 대 한 지원을 SPEES 쿼리에 Python 및 microsoftml의 향상 된 오류 메시지에 포함 합니다. |
| CU 5 | 버그 수정 및 패키지 새로 고침 했지만 공지 새 기능입니다. 수정 함수 및 변수 revoscalepy rxInstallPackages, RxExec rx_exec 함수 및 경고 메시지에 대 한 수정 버전에 대 한 루프백에서 연결을 수정에 긴 경로 관련 오류를 수정 하에 변환의 향상 된 기능을 포함 합니다. |
| CU 4 | 버그 수정 및 패키지 새로 고침 했지만 공지 새 기능입니다. |
| CU 3 | Python 모델의 serialization revoscalepy 사용 하는 [rx_serialize_model 함수](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/><br/>[네이티브 점수 매기기](sql-native-scoring.md) 향상 된 기능 plus [실시간 점수 매기기](real-time-scoring.md)합니다. 데이터베이스 내에 다음이 점수 매기기를 사용 하 여 처리량은 당 행 수는 백만 R 모델을 사용 하 여 두 번째입니다. 실시간 점수 매기기 및 네이티브 점수 매기기는이 업데이트에서 단일 행 및 일괄 처리 점수 매기기에 더 나은 성능을 제공합니다. 사용 하 여 점수 매기기 네이티브 빠른 점수를 매기기 위해는 T-SQL 함수 Linux 에서도 SQL Server의 모든 버전에서 실행할 수 있습니다. 함수에는 R 또는 추가 구성이 없는 설치를 해야합니다. 즉, 다른 곳에서 모델을 학습, SQL Server에서 저장 한 다음 그 어느 때 R.를 호출 하지 않고 점수 매기기를 수행합니다 방법론을 점수 매기기에 대 한 자세한 내용은 참조 하세요. [실시간 점수 매기기 또는 네이티브 점수 매기기를 수행 하는 방법을](r/how-to-do-realtime-scoring.md)합니다. |
| CU 2 | 버그 수정 및 패키지 새로 고침 했지만 공지 새 기능입니다. |
| CU 1 | Revoscalepy, 추가 유사한 SQL Server 데이터 원본에서 스키마 정보를 반환 하는 데 rx_create_col_info [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) r <br/><br/>향상 된 기능 [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) 사용 하 여 병렬 시나리오를 지원 하기는 `RxLocalParallel` 계산 컨텍스트.|
| 초기 릴리스 |[**데이터베이스 내 분석에 대 한 Python 통합**](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/) <br/><br/>합니다 [revoscalepy](python/what-is-revoscalepy.md) 패키지는 RevoScaleR의 Python에 해당 합니다. 선형 및 로지스틱 회귀, 의사 결정 트리, 승격 된 트리 및 임의 포리스트의 모든 병렬 및 원격 계산 컨텍스트에서 실행 되 고 수에 대 한 Python 모델을 만들 수 있습니다. 이 패키지는 여러 데이터 원본 및 원격 계산 컨텍스트 사용을 지원합니다. 데이터 과학자 또는 개발자가 데이터를 탐색 하거나 데이터를 이동 하지 않고 모델을 작성 하는 원격 SQL Server에서 Python 코드를 실행할 수 있습니다. <br/><br/>합니다 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 패키지는 MicrosoftML R 패키지의 Python에 해당 합니다.<br/><br/>T-SQL 및 Python 통합을 통해 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)합니다. 이 저장된 프로시저를 사용 하 여 모든 Python 코드를 호출할 수 있습니다. 이 보안 인프라를 통해 간단한 저장된 프로시저를 사용 하 여 응용 프로그램에서 호출할 수 있는 스크립트 및 Python 모델의 엔터프라이즈급 배포할 수 있습니다. SQL에서 Python 프로세스 및 MPI 링 병렬화로 스트리밍 데이터에서 추가 성능 향상. <br/><br/>T-SQL을 사용할 수 있습니다 [PREDICT](../t-sql/queries/predict-transact-sql.md) 수행 하는 함수 [네이티브 점수 매기기](sql-native-scoring.md) 필요한 이진 형식으로 이전에 저장 하는 미리 학습 된 모델입니다.|
| 초기 릴리스 | [**MicrosoftML (R)** ](using-the-microsoftml-package.md) 크기가 조정 되거나 실행 원격 계산 컨텍스트 수 있는 알고리즘 및 데이터 변환을 학습의 최신 컴퓨터를 포함 합니다. 사용자 지정 가능한 심층 신경망, 빠른 의사 결정 트리 및 의사 결정 포리스트, 선형 회귀 및 로지스틱 회귀 알고리즘에 포함 됩니다. |
| 초기 릴리스 | [**미리 학습 된 모델** ](install/sql-pretrained-models-install.md) 이미지 인식 및 긍정 음수가 감정 분석에 대 한 합니다. 이러한 모델을 사용 하 여 고유의 데이터에서 예측을 생성 합니다. |
| 초기 릴리스 | [**R 패키지 관리**](r/install-additional-r-packages-on-sql-server.md), 다음 중요 정보를 포함 하 여: 데이터베이스 dba가 패키지를 관리 하 고 패키지를 설치 하는 권한을 할당 하는 데 역할 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 를 t-sql로 문 도움말 dba가 R을 알 필요 없이 패키지를 관리 및 다양 한 R 함수가 [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) 설치, 제거 또는 패키지 나열 하는 데 사용자가 소유 합니다. |
| 초기 릴리스 | [**Mrsdeploy 통해 운영 화** ](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package) 배포 하 고 R 스크립트를 웹 서비스로 호스팅. R 스크립트에만 사용 (Python 해당 없음)에 적용 됩니다. 다른 SQL Server 작업과 리소스 경쟁을 방지 하려면 (독립 실행형) 서버 옵션을 위한 것입니다. |


## <a name="new-in-sql-server-2016"></a>SQL Server 2016의에서 새로운 기능

이 릴리스에 도입 된 기계 학습을 통해 SQL server 기능 **SQL Server 2016 R Services**, 데이터베이스 엔진 인스턴스를 내 상주 데이터에 대해 처리 R 스크립트에 대 한 데이터베이스 내 분석 엔진입니다.

또한 **SQL Server 2016 R Server (독립 실행형)** Windows 서버에서 R Server를 설치 하는 방법으로 릴리스 되었습니다. 처음에 SQL Server 설치 프로그램에는 Windows에 대 한 R Server를 설치 하는 유일한 방법은 제공 합니다. 이후 릴리스에서 개발자 및 데이터 과학자의 R Server에 Windows 하고자 했던 동일한 목표를 달성 하려면 다른 독립 실행형 설치 관리자를 사용할 수 있습니다. SQL Server의 독립 실행형 서버는 독립 실행형 서버 제품에 기능적 [Microsoft R Server에 대 한 Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)합니다.

| 릴리스 |기능 업데이트 |
|---------|----------------|
| CU 추가 | [**실시간 점수 매기기** ](real-time-scoring.md) 최적화 된 이진 형식으로 저장 된 모델을 읽고 R 런타임을 호출 하지 않고 예측을 생성할 네이티브 c + + 라이브러리에 의존 합니다. 이렇게 하면 점수 매기기 작업을 훨씬 더 빠릅니다. 실시간 점수 매기기를 사용 하 여 저장된 프로시저를 실행할 수도 있고 실시간 R 코드에서 점수 매기기를 수행할 수 있습니다. 실시간 점수 매기기 역시 사용할 수 있는 SQL Server 2016에 대 한 인스턴스를 최신 릴리스로 업그레이드 되 면 [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]합니다. |
| 초기 릴리스 | [**데이터베이스 내 분석에 R 통합**](r/sql-server-r-services.md)합니다. <br/><br/> 호출 R에 대 한 R 패키지에는 t-sql로 또는 그 반대로 작동 합니다. 관리 분산 처리 및 결과 집계 및 RevoScaleR 함수 조정 구성 요소로 데이터를 청크 하 여 대규모 R 분석을 제공 합니다. SQL Server 2016 R Services (In-database)에서 RevoScaleR 엔진 데이터 및 분석 같은 처리 컨텍스트에서 함께 brining 데이터베이스 엔진 인스턴스를 통합 되어 있습니다. <br/><br/>T-SQL 및 R 통합을 통해 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)합니다. 이 저장된 프로시저를 사용 하 여 R 코드를 호출할 수 있습니다. 이 보안 인프라에 보냈습니다 모델 및 간단한 저장된 프로시저를 사용 하 여 응용 프로그램에서 호출할 수 있는 스크립트의 엔터프라이즈급 배포할을 수 있습니다. SQL에서 R 프로세스 및 MPI 링 병렬화로 스트리밍 데이터에서 추가 성능 향상. <br/><br/>T-SQL을 사용할 수 있습니다 [PREDICT](../t-sql/queries/predict-transact-sql.md) 수행 하는 함수 [네이티브 점수 매기기](sql-native-scoring.md) 필요한 이진 형식으로 이전에 저장 하는 미리 학습 된 모델입니다.|

## <a name="linux-support-roadmap"></a>Linux 지원 로드맵

Linux의 SQL Server에서 R 또는 Python에서 데이터베이스를 사용 하 여 machine learning 현재 지원 되지 않습니다. 이후 릴리스에서 공지를 찾습니다.

그러나 Linux에서 수행할 수 있습니다 [네이티브 점수 매기기](sql-native-scoring.md) T-SQL PREDICT 함수를 사용 하 여 합니다. 네이티브 점수 매기기 호출 또는 심지어는 R 런타임 요구 하지 않고 매우 빠르며 미리 학습 된 모델에서 점수를 매길 수 있습니다. 즉, 클라이언트 응용 프로그램에 맞도록 매우 빠른 예측을 생성 하려면 Linux에서 SQL Server를 사용할 수 있습니다.

<a name="azure-sql-database-roadmap"></a>

## <a name="azure-sql-database-roadmap"></a>Azure SQL Database 로드맵

Azure SQL Database에서 R에 대 한 지원은 제한 됩니다: 프리미엄 계층에서 만든 서비스에 서 부 중앙 미국 에서만 사용할 수 있습니다. Python 지원을 비롯 하 여 확장 된 검사, 향후 릴리스에서 수행 가능성이 있습니다. 그러나이 이번에 출시 될 예정된 날짜 없음는 합니다.  

## <a name="next-steps"></a>다음 단계

+ [SQL Server 2017 Machine Learning Services (In-database) 설치](install/sql-machine-learning-services-windows-install.md)
+ [Machine learning 자습서 및 샘플](tutorials/machine-learning-services-tutorials.md)
