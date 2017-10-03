---
title: "Azure SQL 데이터베이스에서 R을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 619921bbf00801fd5930a1c1b110e69a9fd05a81
ms.contentlocale: ko-kr
ms.lasthandoff: 09/30/2017

---
# <a name="using-r-in-azure-sql-database"></a>Azure SQL 데이터베이스에서 R을 사용 하 여

2017 년 1 년 10 월부터 Azure SQL 데이터베이스는 R 코드에서-데이터베이스의 SQL Server 2016에서 R 서비스와 비슷한 저장된 프로시저를 사용 하 여 실행을 지원 합니다.

이 문서는 기능의 개요를 제공 하 고 알려진된 제한 사항에 설명 합니다.

> [!NOTE]
> 이 릴리스에 초기 미리 보기 버전 하며 테스트 및 탐색만. 프로덕션 버전에 2018 발표 될 됩니다. 정확한 릴리스 날짜 및 빌드 사용자 의견에 따라 달라 집니다. 따라서 사용자 좋습니다 기능을 시도 하 고 있는 중요 한 기능을 알려 주십시오. 
> 
> 릴리스 일정에 대 한 정보를 참조 하십시오.는 [SQL Server 블로그](https://blogs.technet.microsoft.com/dataplatforminsider/) 또는 [Microsoft R Server 블로그](https://blogs.msdn.microsoft.com/rserver/)합니다.

## <a name="features"></a>기능

미리 보기 릴리스는 다음과 같은 기능을 제공합니다.

+ 저장된 프로시저를 사용 하 여 기계 학습 솔루션의 간편한 배포를 위해 R을 호출
+ 클라우드 데이터베이스에 연결할 수 있는 모든 응용 프로그램을 사용 하 여 모델에서 점수를 가져오기
+ 예측 함수를 사용 하 여 R 런타임 사용 하지 않고 빠른 점수 매기기에 대 한 기본 점수 매기기를 지원 합니다.

미리 보기 버전으로 특정 제한에 대 한 참조 [제한 사항 및 알려진된 문제](#bkmk_restrictions)합니다.

### <a name="components"></a>Components

전체 아키텍처는 SQL Server 컴퓨터 R Services의 비슷합니다.

**보안**

+ SQL Server 신뢰할 수 있는 실행 패드의 R 작업 실행을 관리 하 고 프로세스의 수명을 제어 합니다. 

**R 패키지**

+ 미리 보기 릴리스는 Microsoft R Open 3.3.3, 및 Microsoft R Server 버전 9.2 합니다. [RevoScaleR 패키지](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) 미리 설치 되어 있습니다.

+ 일부 R 패키지 제거 되었거나 Azure 환경에서 공간을 줄이고 수정 합니다. 예를 들어 **mrsdeploy** Azure SQL 데이터베이스에 포함 되지 않습니다.

**성능**

+ 교육 하 고 메모리에서 데이터를 처리할 수 있는 모든 모델에서 점수 매기기를 지원 합니다.  데이터베이스의 버전에 사용 가능한 메모리 양에 따라 다릅니다. 
+ Trivial 병렬 처리를 사용 하 여 지원 되는 @parallel 인수 1 = 수 있을 뿐만 아니라 R 스크립트 실행에 대 한 스트리밍 
+ 미리 보기에서 데이터베이스 당 동시에 실행 하는 단일 R 스크립트를 제한 합니다.

**언어들**

이후 버전에 대 한 로드맵 Python 및 추가 패키지에 대 한 지원이 포함 되어 있습니다.

## <a name="restrictions"></a>제한 사항

이 섹션에는 미리 보기 버전에 적용 되는 몇 가지 추가 제한 나열 됩니다.

### <a name="upgrading-r-components-and-adding-packages-not-supported"></a>R 구성 요소를 업그레이드 하 고 지원 되지 않습니다 패키지 추가

Azure SQL 데이터베이스는 관리 되는 서비스 및 R 구성 요소에 대 한 업그레이드를 관리 하는 고객 필요 하지 않습니다. 미리 보기 릴리스에 대 한 사용 가능한 설치 된 패키지를 사용 하십시오.

R 및 다른 기계 학습 구성 요소에 대 한 업그레이드 제공 되 면 해제 됩니다.

### <a name="availability"></a>가용성

R 및 다른 기계 학습에서 Azure SQL 데이터베이스 스크립트를 실행할 수만 중앙 미국 서 부 지역에서 미리 보기 기능은입니다. 예: 서유럽, 다른 지역으로 확장은 이후 릴리스에서 제공 하도록 계획 합니다.

Azure SQL 데이터베이스에서 R 실행 충분 한 저장소와 메모리를 필요 합니다. 현재 다음 데이터베이스 서비스 계층 및 성능 수준이 지원 됩니다.

+ Premium 서비스 계층: P1, P2, P4, P6, P11, P15 
+ Premium RS 서비스 계층: PRS1, PRS2, PRS4 PRS6 
+ 프리미엄 탄력적 풀: 125 Edtu 이상 
+ 프리미엄 RS 탄력적인 풀: 125 Edtu 이상 

### <a name="resource-management"></a>리소스 관리

이 릴리스에서 R 설치를 사용자 지정 하거나 R 스크립트를 사용 하 여 모니터링 하는 기능은 지원 하지 않습니다.

예를 들어 R 스크립트 실행 특정 데이터베이스에 대해서만 사용할 수 없습니다.

R 스크립트의 CPU 및 메모리 사용을 모니터링 하는 데 사용 되는 DMV sys.dm_db_resource_stats 미리 보기 릴리스에서 사용할 수 없는 경우

### <a name="other-limitations"></a>기타 제한 사항

다음과 같은 기능이 지원 되지 않습니다. 

+ MicrosoftML 패키지를 사용할 수 없는 경우
+ 외부 라이브러리 만들기와 같은 패키지 관리 기능을 사용할 수 없습니다.
+ R 클라이언트에서 스크립트를 실행할 때 원격 계산 컨텍스트는 Azure SQL 데이터베이스를 사용할 수 없습니다. 저장된 프로시저 sp_execute_external_script를 사용 하 여 R 스크립트를 실행 해야 합니다. 저장된 프로시저에 의해 호출 되는 스크립트는 다른 계산 컨텍스트를 사용할 수 없습니다.
+ 병렬 실행을 필요로 하는 rx 함수에 대 한 호출을 실행할 수 없습니다.
+ SQL Server R 스크립트에서 루프백 연결을 사용할 수 없습니다. 즉, 다른 ODBC 데이터 원본에 R 스크립트에서 외부 호출을 만들 수 없습니다.

## <a name="get-started"></a>시작

SQL Server 개발 팀에서이 발표에 R 모델을 작성 하 고 예측을 생성 하 여 시험해 사용자의 Azure SQL 데이터베이스에서 실행할 수 있는 간단한 샘플이 포함 됩니다.

+ [학습 및 Azure SQL 데이터베이스의 점수 모델](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-preview-of-machine-learning-services-with-r-support-in-azure-sql-database/)

