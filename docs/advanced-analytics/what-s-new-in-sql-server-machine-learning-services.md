---
title: "어떤&#39;s SQL Server 컴퓨터 학습 서비스의 새로운 기능 | Microsoft Docs"
ms.date: 03/17/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: ee7186be0f28d7df4018b8f94ef661f865179483
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2018
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>SQL Server 컴퓨터 학습 서비스의 새로운 기능 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

컴퓨터 학습 기능을 확장 하 고, 확장 및 데이터 플랫폼 및 데이터 과학, 분석, 간의 통합 향상 시킬 수 각 릴리스에서 SQL Server에 추가 되 고 학습 데이터를 구현 하려면 감독 합니다. 

## <a name="new-in-sql-server-2017"></a>SQL Server 2017의에서 새로운 기능

이 릴리스에서 Python 지원 및 업계를 주도하 기계 학습 알고리즘을 추가 했습니다. 새 범위를 반영 하기 위해 이름이 바뀌었거나, SQL Server 2017 표시 도입 **SQL Server 컴퓨터 학습 Services (In-database)**, Python 및 오른쪽 모두에 대 한 언어 지원 

도 도입 했는데이 릴리스에서 **SQL Server 컴퓨터 학습 서버 (독립 실행형)**, 전용된 시스템에서 실행 하려는 워크 로드를 R 및 Python에 대 한 SQL Server, 완전히 독립적입니다. 독립 실행형 서버를 배포할 수 있으며 SQL Server를 사용 하지 않고 Python 또는 R 솔루션을 확장할 수 있습니다.

| 릴리스 | 기능 업데이트 |
|---------|---------------|
| CU 4 | 버그 수정 및 패키지 새로 고침 있지만 공지 새로운 기능입니다. |
| CU 3 | Python 모델 revoscalepy의 serialization을 사용 하는 [rx_serialize_model 함수](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)합니다.<br/><br/>[기본 점수 매기기](sql-native-scoring.md) 의 향상 된 기능 및 [실시간 점수 매기기](real-time-scoring.md)합니다. 데이터베이스에서 상태 평가 된 처리량은 당는 백만 행 R 모델을 사용 하 여 두 번째입니다. 이 업데이트를 실시간 점수 매기기 및 기본 점수 매기기 단일 행 및 일괄 처리 점수 매기기에 더 나은 성능을 제공 합니다. 사용 하 여 점수 매기기 네이티브 빠른 평가에 T-SQL 함수 Linux에도 SQL Server의 모든 버전에서 실행할 수 있습니다. 함수 또는 추가 구성이 없습니다 설치 되어 있어야 합니다. 즉, 다른 곳에서 모델을 학습, SQL Server에서 저장 한 다음 현재까지 오른쪽을 호출 하지 않고 점수 매기기를 수행 있습니다. 방법론 점수 매기기에 대 한 자세한 내용은 참조 하십시오. [실시간 점수 매기기 또는 기본 점수 매기기를 수행 하는 방법을](r/how-to-do-realtime-scoring.md)합니다. |
| CU 2 | 버그 수정 및 패키지 새로 고침 있지만 공지 새로운 기능입니다. |
| CU 1 | Revoscalepy, 추가 유사한 SQL Server 데이터 원본에서 스키마 정보를 반환 하는 데 rx_create_col_info [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) r <br/><br/>향상 된 기능 [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) 를 사용 하 여 병렬 시나리오를 지원 하기는 `RxLocalParallel` 계산 컨텍스트.|
| 초기 릴리스 |[**데이터베이스에서 분석에 대 한 Python 통합**](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/) <br/><br/>[revoscalepy](python/what-is-revoscalepy.md) 패키지는 RevoScaleR Python 동일 합니다. 선형 및 로지스틱 회귀, 의사 결정 트리, 승격 된 트리 및 임의 포리스트 모든 병렬화 하 고 원격 연산 컨텍스트로에서 실행 되 고 수에 대 한 Python 모델을 만들 수 있습니다. 이 패키지의 여러 데이터 소스 및 원격 계산 컨텍스트 사용을 지원합니다. 데이터 과학자 또는 개발자가 데이터를 탐색 하거나 데이터를 이동 하지 않고 모델을 작성 합니다. 원격 SQL Server에서 Python 코드를 실행할 수 있습니다. <br/><br/>[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 패키지는 MicrosoftML R 패키지 Python 동일 합니다.<br/><br/>T-SQL 및 Python 통합을 통해 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)합니다. 이 저장된 프로시저를 사용 하 여 모든 Python 코드를 호출할 수 있습니다. 이 보안 인프라 Python 모델 및 간단한 저장된 프로시저를 사용 하 여 응용 프로그램에서 호출할 수 있는 스크립트의 엔터프라이즈 수준의 배포를 사용 합니다. Python 및 MPI 링 병렬화 SQL는 스트리밍 데이터 추가 성능 향상. <br/><br/>T-SQL을 사용할 수 있습니다 [PREDICT](../t-sql/queries/predict-transact-sql.md) 수행 하는 함수 [기본 점수 매기기](sql-native-scoring.md) 필요한 이진 형식으로 이전에 저장 된 미리 학습 된 모델에 있습니다.|
| 초기 릴리스 | [**MicrosoftML (R)** ](using-the-microsoftml-package.md) 학습 알고리즘 및 데이터 변환 크기 조정 된 또는 실행 원격 계산 컨텍스트를 될 수 있는 최신 상태 컴퓨터를 포함 합니다. 알고리즘은 사용자 지정 가능한 심층 신경망, 빠른 의사 결정 트리 및 의사 결정 포리스트, 선형 회귀, 로지스틱 회귀를 포함 됩니다. |
| 초기 릴리스 | [**미리 학습 된 모델** ](r/install-pretrained-models-sql-server.md) 이미지 인식 및 긍정 음수가 감성 분석에 대 한 합니다. 자신만 데이터에 대 한 예측을 생성 하려면 이러한 모델을 사용 합니다. |
| 초기 릴리스 | [**관리 패키지**](r/r-package-management-for-sql-server-r-services.md), 다음과 같은 주요 기능과 포함 하 여: 데이터베이스 dba가 패키지 관리 패키지를 설치할 권한을 할당할 수 있도록 역할 [외부 라이브러리 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 에 t-sql 문 도움말 Dba R, 알 필요 없이 패키지를 관리 및 다양 한 R 함수가 [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) 설치, 제거 또는 패키지 나열 하려면 사용자가 소유 합니다. |
| 초기 릴리스 | [**Mrsdeploy 통해 해결해줍니다** ](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package) 배포 하 고 R 스크립트를 웹 서비스로 호스팅에 대 한 합니다. R 스크립트에만 사용 (Python 해당 키 없음)에 적용 됩니다. 독립 실행형 서버 옵션 다른 SQL Server 작업과 리소스 경합을 방지 하기 위한 것입니다. |


## <a name="new-in-sql-server-2016"></a>SQL Server 2016의에서 새로운 기능

이 릴리스에 도입 된 시스템 기능을 통해 SQL Server에 학습 **SQL Server 2016 R Services**, 데이터베이스 엔진 인스턴스 내 상주 데이터에 대해 처리 R 스크립트는 데이터베이스 내 분석 엔진입니다.

또한 **SQL Server 2016 R 서버 (독립 실행형)** R 서버 Windows 서버에 설치 하는 방법으로 릴리스 되었습니다. 처음에 SQL Server 설치 프로그램에 Windows 용 R 서버를 설치 하는 유일한 방법은 제공 합니다. 이후 릴리스에서 개발자와 원하는 Windows에서 R Server는 데이터 과학자 같은 목표를 달성 하기 위해 다른 독립 실행형 설치 관리자를 사용할 수 있습니다. SQL Server의 독립 실행형 서버는 독립 실행형 서버 제품으로 [Windows 용 Microsoft R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)합니다.

| 릴리스 |기능 업데이트 |
|---------|----------------|
| CU | [**실시간 점수 매기기** ](real-time-scoring.md) 최적화 된 이진 형식으로 저장 된 모델을 읽고은 R 런타임을 호출 하지 않고 예측을 생성할 네이티브 c + + 라이브러리에 의존 합니다. 이렇게 하면 점수 매기기 작업 훨씬 빠릅니다. 실시간 점수 매기기와 저장된 프로시저를 실행할 수도 있고 실시간 R 코드에서 점수 매기기를 수행할 수 있습니다. 실시간 점수 매기기는 최신 버전에는 인스턴스를 업그레이드 하는 경우 SQL Server 2016 가능 [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]합니다. |
| 초기 릴리스 | [**데이터베이스에서 분석에 대 한 R 통합**](r/sql-server-r-services.md)합니다. <br/><br/> 호출 R에 대 한 R 패키지는 T-SQL, 그 반대로 작동 합니다. 조정 구성 요소 부분으로 구성 데이터를 청크 하 여 규모에 R 분석을 제공 하는 RevoScaleR 함수 및 분산 처리 및 결과 집계를 관리 합니다. SQL Server 2016 R Services (In-database)에서 RevoScaleR 엔진 brining 데이터 및 분석에서 동일한 처리 컨텍스트는 데이터베이스 엔진 인스턴스 통합 되어 있습니다. <br/><br/>T-SQL과 R 통합을 통해 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)합니다. 이 저장된 프로시저를 사용 하 여 모든 R 코드를 호출할 수 있습니다. 이 보안 인프라 보냈습니다 모델 및 간단한 저장된 프로시저를 사용 하 여 응용 프로그램에서 호출할 수 있는 스크립트의 엔터프라이즈 수준의 배포를 사용 합니다. R 프로세스 및 MPI 링 병렬화 SQL는 스트리밍 데이터 추가 성능 향상. <br/><br/>T-SQL을 사용할 수 있습니다 [PREDICT](../t-sql/queries/predict-transact-sql.md) 수행 하는 함수 [기본 점수 매기기](sql-native-scoring.md) 필요한 이진 형식으로 이전에 저장 된 미리 학습 된 모델에 있습니다.|

## <a name="linux-support-roadmap"></a>Linux 지원 로드맵

기계 학습 Python 또는 R에서 데이터베이스를 사용 하 여 Linux에서 SQL Server에서 현재 지원 되지 않습니다. 이후 릴리스에서 공지를 찾습니다.

그러나 Linux에서 수행할 수 있습니다 [기본 점수 매기기](sql-native-scoring.md) T-SQL 예측 함수를 사용 하 여 합니다. 기본 점수 매기기를 호출 하거나 R 런타임도 요구 하지 않고 매우 빠르게 미리 학습 된 모델에서 점수를 매길 수 있습니다. 즉, Linux에서 SQL Server를 사용 하 여 클라이언트 응용 프로그램 역할을 매우 빠르게 예측을 생성할 수 있습니다.

## <a name="next-steps"></a>다음 단계

+ [SQL Server 2017 기계 학습 Services (In-database) 설치](install/sql-machine-learning-services-windows-install.md)
+ [컴퓨터 학습 자습서 및 샘플](tutorials/machine-learning-services-tutorials.md)
