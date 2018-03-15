---
title: "SQL Server 컴퓨터 학습 서비스 버전 간 기능 가용성 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 16ca6c44b15c9fb7c1983d5a04175ebbade57895
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>SQL Server 컴퓨터 학습 서비스의 버전 간 기능 가용성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 컴퓨터 학습 기능은 SQL Server 2016 및 SQL Server 2017에서 사용할 수 있습니다. 이 문서 기능을 제공 하는 버전을 나열 하 고, 특정 버전에 적용 되는 제한 사항을 설명, 특정 버전에만 사용할 수 있는 기능을 나열 합니다.

 > [!NOTE]
 > 일반적으로 SQL Server 기계 학습 (In-database) 포함 하지 않습니다는 [해결해줍니다](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) 독립 실행형 R 서버 또는 컴퓨터 학습 서버 설치에에서 포함 된 기능을 합니다. 해결해줍니다 웹 서비스 배포 및 호스팅, 포함 되어 있으며 다른 SQL Server 작업과와 동일한 리소스에 대 한 경합 때문입니다.
 > 
 > 이러한 이유로 웹 서비스로 예측 모델의 배포를 지원 하기 위해 다른 실제 서버에 SQL Server 2016 R 서버 (독립 실행형) 또는 SQL Server 2017 컴퓨터 학습 서버 (독립 실행형) 설치 하는 것이 좋습니다. 

## <a name="sql-server-2017-machine-learning-services-in-database-and-standalone"></a>SQL Server 2017 컴퓨터 학습 Services (In-database) 및 (독립 실행형)

Developer Edition Enterprise Edition의 것과 동일한 성능을 제공합니다. Developer Edition을 사용 하 여 프로덕션 환경에 대해 지원 되지 않습니다.

|기능|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------|----------|--------|---|------------------------------|-------|
| R 인터프리터 & 독점 패키지 | 예 | 사용자 계정 컨트롤 | 아니요 | 아니오 | 아니요 | 
| Python 인터프리터 & 클라이언트 라이브러리 | 예 | 사용자 계정 컨트롤 | 아니요 | 아니오 | 아니요 | 
| 데이터 청크 <br/>(처리 많은 양의 데이터를 메모리에 적합 하는 한도 초과 하지 않음) | 예 | 아니요 | 아니오 | 아니오 | 아니요 |
| 수직 처리 <br/>(2 개 이상 프로세서) | 예 | 아니요 | 아니오 | 아니오 | 아니요 |
| 화 | 예 | 아니요 | 아니오 | 아니오 | 아니요 |
| [예측](../../t-sql/queries/predict-transact-sql.md) 함수 <br/>(수행 [기본 점수 매기기](../sql-native-scoring.md) 필요한 이진 형식으로 이전에 저장 된 미리 학습 된 모델에 대해) | 예 | 사용자 계정 컨트롤 | 사용자 계정 컨트롤 | 사용자 계정 컨트롤 | 예 |
| R 클라이언트 호환성 | 예 | 사용자 계정 컨트롤 | 아니요 | 아니오 | 아니요 | 
| Microsoft R Open | 예 | 사용자 계정 컨트롤 | 아니요 | 아니오 | 아니요 | 
| Anaconda Python 3.5 | 예 | 사용자 계정 컨트롤 | 아니요 | 아니오 | 아니요 | 

## <a name="sql-server-2016-r-services-in-database-and-r-server-standalone"></a>SQL Server 2016 R Services (In-database) 및 R Server (독립 실행형)

기능 가용성 2017 년 1 2016 처음 릴리스에 속하지는 Python 지원 빼기와 같습니다.

## <a name="r-feature-availability-in-azure-sql-database"></a>Azure SQL 데이터베이스에서 지원 되는 R 기능
  
초기 테스트 릴리스 후 R 서비스는 현재 **하지** 이후 개발 보류 중인 Azure SQL 데이터베이스에서 사용할 수 있습니다. 

## <a name="performance-expectations-for-enterprise-edition"></a>Enterprise Edition에 대 한 성능 기대

컴퓨터 학습 솔루션의 성능을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 초과 하는 동일한 하드웨어를 지정 된 기존 R을 사용 하 여 이전에 일반적으로 사용할 수 있습니다. SQL Server에서 R 솔루션 수 실행할 수 때문에 서버 리소스를 사용 하 여이 하 고 경우에 따라 사용 하 여 여러 프로세스에 배포 하는 **RevoScaleR** 함수입니다. 

기능은 아직 개발 중인 되지만 적용 것으로 예상 되는 동일한 이점 성능 Python 솔루션에 대 한 평가 된가 합니다.

또한 사용자가 성능 및 학습 솔루션 vs Enterprise Edition에서에서 실행 되는 경우 동일한 컴퓨터에 대 한 확장성에 상당한 차이가 있음을 확인할 예상할 수 있습니다. 확인할 수 있습니다. 이유는 RevoScaleR 함수를 메모리에 맞출 수 있는 양보다 더 많은 데이터를 처리할 수 있는 병렬 기계 학습에 사용할 수 있는 증가 된 스레드를 처리 하 고 스트리밍 또는 (청크)에 대 한 지원이 포함 됩니다. 

그러나 동일한 하드웨어에도 성능 R, Python 코드 외부 요인에 따라 달라질 수 있습니다. 이러한 요소에는 서버 리소스에 대 한 경쟁 요청, 생성 되는 쿼리 계획의 형식, 스키마 변경 내용을 포함 한 통계를 업데이트 또는 새 쿼리 계획을 만든, 조각화가 필요 합니다. 저장된 프로시저 또는 Python 코드가 포함 된가 초 하나의 작업에서 실행 되지만 걸릴 때을 분 수 다른 서비스를 실행 합니다.  따라서 여러 가지 컴퓨터 학습 성과 측정 하는 경우에 원격 계산 컨텍스트에 대 한 네트워킹을 포함 하 여 서버 성능 모니터링 하는 것이 좋습니다.

구성 하는 것이 좋습니다 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md) (Enterprise Edition에서 사용 가능) 외부 스크립트 작업은 우선 순위를 지정 또는 많은 서버 워크 로드에서 처리 하는 방법을 사용자 지정할 수 있습니다. 외부 스크립트 작업의 원본을 지정 하 고 특정 작업 우선 순위를 지정 하 고, SQL 쿼리를 사용 하는 메모리의 양을 제한 하는 분류자 함수를 정의 하 고 작업 단위로 사용 되는 병렬 프로세스의 수를 제어할 수 있습니다.

## <a name="see-also"></a>참고 항목

+ [버전 및 SQL Server 2016 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [버전 및 SQL Server 2017 구성 요소](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [R (컴퓨터 학습 서버)에서 큰 데이터로 컴퓨팅에 대 한 팁](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
