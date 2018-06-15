---
title: SQL Server 컴퓨터 학습 서비스 버전 간 기능 가용성 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cdb3e54addb2137e7c0ae2d6462be9c75c542539
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31201925"
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>SQL Server 컴퓨터 학습 서비스의 버전 간 기능 가용성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 컴퓨터 학습 기능은 SQL Server 2016 및 SQL Server 2017에서 사용할 수 있습니다. 이 문서 기능을 제공 하는 버전을 나열 하 고, 특정 버전에 적용 되는 제한 사항을 설명, 특정 버전에만 사용할 수 있는 기능을 나열 합니다.


## <a name="sql-server-2017-features"></a>SQL Server 2017 기능

Enterprise 및 Developer 버전의 동일한 기능 범위를 추가 하는 동일한 비용이 발생 하지 않고 엔터프라이즈 설치에 대 한 솔루션을 빌드할 수 있습니다 됩니다. 버전 영역은 기능적으로 동일 하지만 Developer Edition을 사용 하 여 프로덕션 환경에 대해 지원 되지 않습니다.

기본 및 고급 통합 간의 차이점은 배율입니다. 고급 integration 컴퓨터를 수용할 수 있는 모든 크기로 데이터 집합의 병렬 처리에 대 한 모든 사용 가능한 코어를 사용할 수 있습니다. 기본 통합은 메모리에 맞는 데이터 집합 2 개의 코어로 제한 합니다. 

기본 및 고급 통합 (In-database) 인스턴스에 적용 됩니다. 독립 실행형 서버는 데이터베이스 엔진 인스턴스 기능 아니며 Developer 및 Enterprise edition에만 설치 옵션으로 제공 됩니다.

|기능|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|기본 R 통합|예|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|아니요|   
|고급 R 통합|예|아니요|아니오|아니오|아니요| 
|기본 Python 통합|예|사용자 계정 컨트롤|사용자 계정 컨트롤|사용자 계정 컨트롤|아니요|
|고급 Python 통합|예|아니요|아니오|아니오|아니요| 
|Machine Learning Server(독립 실행형)|예|아니요|아니오|아니오|아니요|   

 > [!NOTE]
 > (독립 실행형) 서버 한 대만 제공는 [해결해줍니다](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) Microsoft (SQL-브랜드가 지정 되지 않은) R 서버 또는 컴퓨터 학습 서버 설치에 포함 된 기능을 합니다. 해결해줍니다 웹 서비스 배포 및 호스팅 기능을 포함 합니다.
>
> (In-database) 설치의 경우 솔루션 작업 활용 하는 해당 하는 방법은 활용 하 여 데이터베이스 엔진의 기능 저장된 프로시저에서 실행할 수 있는 함수에 코드를 변환할 때.


## <a name="sql-server-2016-r-features"></a>SQL Server 2016 R 기능

SQL Server 2016 R 통합만 포함 되어 있습니다. SQL Server 2016의 기본 및 고급 R 통합 SQL Server 2017와 동일 합니다.

## <a name="r-feature-availability-in-azure-sql-database"></a>Azure SQL 데이터베이스에서 지원 되는 R 기능
  
초기 테스트 릴리스 후 추가 개발 보류 중인 R 서비스는 Azure SQL 데이터베이스에서 제거 되었습니다. 

## <a name="performance-expectations-for-enterprise-edition"></a>Enterprise Edition에 대 한 성능 기대

컴퓨터 학습 솔루션의 성능을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 초과 하는 동일한 하드웨어를 지정 된 기존 R을 사용 하 여 이전에 일반적으로 사용할 수 있습니다. SQL Server에서 R 솔루션 수 실행할 수 때문에 서버 리소스를 사용 하 여이 하 고 경우에 따라 사용 하 여 여러 프로세스에 배포 하는 **RevoScaleR** 함수입니다. 

또한 사용자가 성능 및 학습 솔루션 vs Enterprise Edition에서에서 실행 되는 경우 동일한 컴퓨터에 대 한 확장성에 상당한 차이가 있음을 확인할 예상할 수 있습니다. 확인할 수 있습니다. 이유는 RevoScaleR 함수를 메모리에 맞출 수 있는 양보다 더 많은 데이터를 처리할 수 있는 병렬 기계 학습에 사용할 수 있는 증가 된 스레드를 처리 하 고 스트리밍 또는 (청크)에 대 한 지원이 포함 됩니다. 

그러나 동일한 하드웨어에도 성능 R, Python 코드 외부 요인에 따라 달라질 수 있습니다. 이러한 요소에는 서버 리소스에 대 한 경쟁 요청, 생성 되는 쿼리 계획의 형식, 스키마 변경 내용을 포함 한 통계를 업데이트 또는 새 쿼리 계획을 만든, 조각화가 필요 합니다. 저장된 프로시저 또는 Python 코드가 포함 된가 초 하나의 작업에서 실행 되지만 걸릴 때을 분 수 다른 서비스를 실행 합니다.  따라서 여러 가지 컴퓨터 학습 성과 측정 하는 경우에 원격 계산 컨텍스트에 대 한 네트워킹을 포함 하 여 서버 성능 모니터링 하는 것이 좋습니다.

구성 하는 것이 좋습니다 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md) (Enterprise Edition에서 사용 가능) 외부 스크립트 작업은 우선 순위를 지정 또는 많은 서버 워크 로드에서 처리 하는 방법을 사용자 지정할 수 있습니다. 외부 스크립트 작업의 원본을 지정 하 고 특정 작업 우선 순위를 지정 하 고, SQL 쿼리를 사용 하는 메모리의 양을 제한 하는 분류자 함수를 정의 하 고 작업 단위로 사용 되는 병렬 프로세스의 수를 제어할 수 있습니다.

## <a name="see-also"></a>참고 항목

+ [버전 및 SQL Server 2016 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [버전 및 SQL Server 2017 구성 요소](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [R (컴퓨터 학습 서버)에서 큰 데이터로 컴퓨팅에 대 한 팁](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
