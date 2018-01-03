---
title: "SQL Server의 기계 학습에 대 한 리소스 관리 | Microsoft Docs"
ms.custom: 
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 61cffc85e6a27ffe4c171da8849d84a19332f223
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>SQL Server의 기계 학습에 대 한 리소스 관리

이 문서를 할당 하 고 R 및 Python 스크립트를 사용 하는 리소스를 분산 하는 SQL Server의 기능 리소스 관리에 대 한 개요를 제공 합니다.

**적용 대상:** [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] 
 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] 및 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]

## <a name="goals-of-resource-governance-for-machine-learning"></a>기계 학습에 대 한 리소스 거 버 넌 스의 목표

중요 한 한 R, Python 등의 시스템 학습 언어를 사용 하 여 알려진된 문제점 점을 의해 제어 되지 컴퓨터에 데이터는 데이터베이스 외부의 자주 이동 IT 합니다. 다른은 R 단일 스레드 이며 메모리에 사용할 수 있는 데이터와 함께 작동만 수 있습니다. 

이러한 두 문제를 완화 하는 SQL Server 컴퓨터 학습 서비스 및 엔터프라이즈 준수 요구 사항을 충족 합니다. 데이터베이스 내부에 고급 분석을 유지 하 고 큰 데이터 집합 스트리밍 청크 작업 등의 기능을 통해 성능이 향상된 시킬 수 있도록 지원 합니다. R 및 Python 계산 데이터베이스 내를 이동 합니다. 일반 사용자 쿼리, 외부 응용 프로그램 및 예약 된 데이터베이스 작업을 포함 하 여 데이터베이스를 사용 하는 다른 서비스의 성능 영향을 수 있습니다.

이 섹션에서는 R 및 Python 등의 외부 런타임 다른 핵심 데이터베이스 서비스에 대 한 영향을 완화 하기 위해 사용 하는 리소스를 관리 하는 방법에 대 한 정보를 제공 합니다. 데이터베이스 서버 환경에는 일반적으로 여러 종속 응용 프로그램 및 서비스에 대 한 허브입니다.

사용할 수 있습니다 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md) R 및 Python에 대 한 외부 런타임 사용 하는 리소스를 관리할 수 있습니다.  기계 학습 리소스 관리에는 이러한 작업이 포함 됩니다.

+ 과도한 서버 리소스를 사용하는 스크립트 식별.
  
     관리자는 너무 많은 리소스를 사용하고 있는 작업을 종료하거나 제한할 수 있어야 합니다.
  
+ 예기치 않은 작업 줄이기.
  
     예를 들어 서버에서 동시에 실행 중인 여러 컴퓨터 학습 작업이 경우 결과 리소스 경합 수 예측할 수 없는 성능이 되 또는 작업의 완료를 위협입니다. 그러나 리소스 풀을 사용 하는 경우 작업 서로 격리 될 수 있습니다.
  
-   작업 우선 순위 지정.
  
     관리자 또는 설계자, 우선 순위가 높은 또는 특정 작업을 완료 하려면 리소스 경합이 있을 때 보장 해야 하는 작업을 지정할 수 해야 합니다.

## <a name="how-to-use-resource-governor-to-manage-machine-learning"></a>기계 학습을 관리 하려면 리소스 관리자를 사용 하는 방법
 
만들어 Python 또는 R 세션에 할당 된 리소스 관리는 *외부 리소스 풀*, 풀 또는 풀에 작업을 할당 합니다. 외부 리소스 풀은 리소스 풀에 도입 된 새로운 유형의 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] R 런타임 및 기타 관리를 위해 데이터베이스 엔진에 외부를 처리 합니다.

SQL Server에서는 세 가지 유형의 기본 리소스 풀을 지원합니다. 
  
-   *내부 풀*은 SQL Server 자체에서 사용되는 리소스를 나타내고 변경하거나 제한할 수 없습니다.
  
-   *기본 풀*은 서버에 대한 리소스 사용을 전체적으로 수정하는 데 사용할 수 있는 미리 정의된 사용자 풀입니다. 이 풀에 속한 사용자 그룹을 정의하여 리소스에 대한 액세스를 관리할 수도 있습니다.
  
-   *기본 외부 풀*은 외부 리소스용으로 미리 정의된 사용자 풀입니다. 새 외부 리소스 풀을 만들고 이 풀에 속하는 사용자 그룹을 정의할 수도 있습니다.
  
 또한 *사용자 정의 리소스 풀*을 만들어 데이터베이스 엔진 또는 기타 응용 프로그램에 리소스를 할당하고 *사용자 정의 외부 리소스 풀*을 만들어 R 및 기타 외부 프로세스를 관리할 수 있습니다.
  
 용어 및 일반적인 개념에 대한 자세한 내용은 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)을 참조하세요.

  
## <a name="resource-management-walkthrough-with-resource-governor"></a>리소스 관리 연습을 리소스 관리자

리소스 관리자를 처음 이라면 빠른 인스턴스 기본 리소스를 수정 하 고 새 외부 리소스 풀을 만들려면 방법 연습 하려면 다음이 항목을 참조 하십시오.: [외부 스크립트에 대 한 리소스 풀 만들기](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)
  
 사용할 수는 *외부 리소스 풀* 기계 학습에 사용 되는 다음 실행 파일에서 사용 하는 리소스를 관리 하는 메커니즘.

+ Rterm.exe 및 위성 프로세스
+ Python.exe 및 위성 프로세스
+ BxlServer.exe 및 위성 프로세스
+ 실행 패드를 통해 시작 하는 위성 프로세스
  
> [!NOTE]
> 
> 리소스 관리자를 사용 하 여 실행 패드 서비스에 대 한 직접 관리 지원 되지 않습니다. 이는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]는 디자인상 Microsoft에서 제공하는 시작 관리자만 호스트할 수 있는 신뢰할 수 있는 서비스이기 때문입니다. 신뢰할 수 있는 아이콘은 과도 한 리소스를 사용 하지 않도록 구성 됩니다.
>   
> 리소스 관리자를 사용하여 위성 프로세스를 관리하고 개별 데이터베이스 구성 및 작업의 요구 사항에 맞게 조정하는 것이 좋습니다.  예를 들어 실행하는 동안 요청 시 개별 위성 프로세스를 만들거나 제거할 수 있습니다.
  
## <a name="disable-external-script-execution"></a>외부 스크립트 실행을 사용 하지 않도록 설정

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 시 외부 스크립트 지원은 선택 사항입니다. 기계 학습 기능을 설치한 후에 기본적으로 외부 스크립트를 실행 하는 기능은 OFF이 고 수동으로 속성을 다시 구성 하 고 스크립트 실행을 활성화 하려면 인스턴스를 다시 시작 해야 합니다.

따라서 즉시 완화 되어야 하는 리소스 문제 또는 보안 문제가 있는 경우 관리자가 즉시 해제할 수 있는 외부 스크립트 실행을 사용 하 여 [sp_configure &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 속성을 설정 하 고 `external scripts enabled` FALSE 또는 0입니다.
  
## <a name="see-also"></a>관련 항목:

[기계 학습 솔루션 관리 및 모니터링](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

[기계 학습을 위한 리소스 풀 만들기](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

[리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
