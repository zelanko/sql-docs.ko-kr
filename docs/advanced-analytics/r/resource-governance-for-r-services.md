---
title: "R Services에 대한 리소스 관리 | Microsoft 문서"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5475c2258971c48c2e19bba69d9ec962ae48be87
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="resource-governance-for-r-services"></a>R Services에 대한 리소스 관리
  R의 한 가지 취약점은 프로덕션에서 대용량 데이터를 분석하려면 추가 하드웨어가 필요하고 데이터가 종종 데이터베이스 외부의 IT 부서에서 관리하지 않는 컴퓨터로 이동된다는 것입니다.  고급 분석 작업을 수행하려면 고객은 데이터베이스 서버 리소스를 이용해야 하고 데이터를 보호하려면 해당 작업이 보안 및 성능과 같은 엔터프라이즈급 준수 요구 사항을 충족하도록 해야 합니다.  
  
 이 섹션에서는 R 런타임에서 사용되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 계산 컨텍스트로 사용하여 실행되는 R 작업에서 사용되는 리소스를 관리하는 방법을 설명합니다.  
  
## <a name="what-is-resource-governance"></a>리소스 관리란?  
 리소스 관리는 보통 지원 및 균형 유지를 위한 여러 서비스 및 여러 종속 응용 프로그램이 있는 데이터베이스 서버 환경에서 일반적으로 발생하는 문제를 식별하고 방지하도록 디자인되어 있습니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 경우 리소스 관리에는 다음 태스크가 포함됩니다.  
  
-   과도한 서버 리소스를 사용하는 스크립트 식별.  
  
     관리자는 너무 많은 리소스를 사용하고 있는 작업을 종료하거나 제한할 수 있어야 합니다.  
  
-   예기치 않은 작업 줄이기.  
  
     예를 들어 여러 R 작업이 동시에 서버에서 실행 중이고 작업이 리소스 풀을 통해 서로 격리되지 않는 경우 결과 리소스 경합으로 인해 성능을 예측할 수 없거나 작업이 완료되지 않을 수 있습니다.  
  
-   작업 우선 순위 지정.  
  
     관리자나 설계자는 우선 수행해야 하는 작업을 지정하거나 리소스 경합이 있는 경우 특정 작업이 완료되도록 보장할 수 있어야 합니다.  
  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서는 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)를 사용하여 R 런타임 및 원격 R 작업에서 사용되는 리소스를 관리할 수 있습니다.  
  
## <a name="how-to-use-resource-governor-to-manage-r-jobs"></a>리소스 관리자를 사용하여 R 작업을 관리하는 방법  
 일반적으로 R 작업에 할당된 리소스를 관리하려면 *외부 리소스 풀*을 만들고 풀에 작업을 할당합니다. 외부 리소스 풀은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 추가된 새로운 유형의 리소스 풀로, 데이터베이스 엔진 외부의 R 런타임 및 기타 프로세스를 관리하는 데 사용됩니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에는 현재 세 가지 유형의 기본 리소스 풀이 있습니다.  
  
-   *내부 풀*은 SQL Server 자체에서 사용되는 리소스를 나타내고 변경하거나 제한할 수 없습니다.  
  
-   *기본 풀*은 서버에 대한 리소스 사용을 전체적으로 수정하는 데 사용할 수 있는 미리 정의된 사용자 풀입니다. 이 풀에 속한 사용자 그룹을 정의하여 리소스에 대한 액세스를 관리할 수도 있습니다.  
  
-   *기본 외부 풀*은 외부 리소스용으로 미리 정의된 사용자 풀입니다. 새 외부 리소스 풀을 만들고 이 풀에 속하는 사용자 그룹을 정의할 수도 있습니다.  
  
 또한 *사용자 정의 리소스 풀*을 만들어 데이터베이스 엔진 또는 기타 응용 프로그램에 리소스를 할당하고 *사용자 정의 외부 리소스 풀*을 만들어 R 및 기타 외부 프로세스를 관리할 수 있습니다.  
  
 용어 및 일반적인 개념에 대한 자세한 내용은 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)을 참조하세요.  

  
## <a name="resource-management-using-resource-governor"></a>리소스 관리자를 사용한 리소스 관리 

   리소스 관리자를 처음 사용하는 경우 인스턴스 기본 리소스를 수정하고 새 외부 리소스 풀을 만드는 방법에 대한 간단한 연습을 확인하려면 [방법: R에 대한 리소스 풀 만들기](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md) 항목을 참조하세요.   
  
 *외부 리소스 풀* 메커니즘을 사용하여 다음 R 실행 파일에서 사용되는 리소스를 관리할 수 있습니다.  
  
-   Rterm.exe 및 위성 프로세스  
  
-   BxlServer.exe 및 위성 프로세스  
  
-   실행 패드에서 시작된 위성 프로세스  
  
 하지만 리소스 관리자를 사용하여 실행 패드 서비스를 직접 관리자는 작업은 지원되지 않습니다. 이는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]는 디자인상 Microsoft에서 제공하는 시작 관리자만 호스트할 수 있는 신뢰할 수 있는 서비스이기 때문입니다. 과도한 리소스 사용을 피하기 위해 신뢰할 수 있는 시작 관리자도 구성됩니다.  
  
 리소스 관리자를 사용하여 위성 프로세스를 관리하고 개별 데이터베이스 구성 및 작업의 요구 사항에 맞게 조정하는 것이 좋습니다.  예를 들어 실행하는 동안 요청 시 개별 위성 프로세스를 만들거나 제거할 수 있습니다.  
  
## <a name="disable-external-script-execution"></a>외부 스크립트 실행 사용 안 함  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 시 외부 스크립트 지원은 선택 사항입니다. [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]를 설치한 후에도 외부 스크립트를 실행하는 기능은 기본적으로 꺼져 있으므로 수동으로 속성을 다시 구성하고 인스턴스를 다시 시작하여 스크립트 실행을 사용하도록 설정해야 합니다.  
  
 따라서 즉시 해결해야 하는 리소스 문제 또는 보안 문제가 있는 경우 관리자는 즉시 [sp_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용하고 `external scripts enabled` 속성을 FALSE 또는 0으로 설정하여 외부 스크립트 실행을 사용하지 않도록 설정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [R 솔루션 관리 및 모니터링](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [방법: R에 대한 리소스 풀 만들기](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  


