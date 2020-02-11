---
title: 유지 관리 계획 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- SQL12.AG.MAINTPLAN.LEGACY.F1
helpviewer_keywords:
- maintenance plans [SQL Server], about database maintenance plans
- maintenance plans [SQL Server], database compatibility level displayed in designer
- maintenance plans [SQL Server]
ms.assetid: 5982ca65-74fe-44e3-aef9-00a65a0db169
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0643c6fbf8e9a6aa649d4d335117bcb4f5b35208
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68206855"
---
# <a name="maintenance-plans"></a>유지 관리 계획
  유지 관리 계획은 데이터베이스를 최적화하고 정기적으로 백업하며 불일치를 제거하는 데 필요한 태스크의 워크플로를 만듭니다. 유지 관리 계획 마법사에서도 중요한 유지 관리 계획을 만들지만 이러한 계획을 수동으로 만들면 유연성을 향상시킬 수 있습니다.  
  
## <a name="benefits-of-maintenance-plans"></a>유지 관리 계획의 이점  
 [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)]의 유지 관리 계획은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에이전트 작업으로 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 패키지를 만듭니다. 유지 관리 계획은 예약된 간격으로 수동 또는 자동으로 실행될 수 있습니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 유지 관리 계획에서는 다음 기능을 제공합니다.  
  
-   다양한 일반 유지 관리 태스크를 사용한 워크플로 만들기. 사용자 고유의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 만들 수도 있습니다.  
  
-   개념 계층. 각 계획을 통해 태스크 워크플로를 만들거나 편집할 수 있습니다. 각 계획의 태스크를 서로 다른 시간에 실행되도록 예약할 수 있는 하위 계획으로 그룹화할 수 있습니다.  
  
-   마스터 서버/대상 서버 환경에서 사용할 수 있는 다중 서버 계획에 대한 지원  
  
-   원격 서버에 계획 기록을 로깅하는 작업에 대한 지원  
  
-   Windows 인증 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 지원 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="maintenace-plan-functionality"></a>유지 관리 계획 기능  
 다음 태스크를 수행하도록 유지 관리 계획을 만들 수 있습니다.  
  
-   새로운 채우기 비율을 사용하여 인덱스를 다시 만들어 데이터 및 인덱스 페이지에서 데이터를 재구성합니다. 새로운 채우기 비율을 사용하여 인덱스를 다시 만들면 데이터베이스 페이지에 동일하게 분산된 데이터와 사용 가능한 공간이 포함됩니다. 또한 향후 더 빠르게 증가되도록 할 수 있습니다. 자세한 내용은 [인덱스의 채우기 비율 지정](../indexes/specify-fill-factor-for-an-index.md)을 참조하세요.  
  
-   빈 데이터베이스 페이지를 삭제하여 데이터 파일을 압축합니다.  
  
-   쿼리 최적화 프로그램에 테이블 내 데이터 값의 배포에 대한 최신 정보가 있는지 확인하도록 인덱스 통계를 업데이트합니다. 따라서 쿼리 최적화 프로그램은 데이터베이스에 저장된 데이터에 대한 더 많은 정보를 갖게 되므로 데이터에 대한 최상의 액세스 방법을 더 잘 판단할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 정기적으로 인덱스 통계를 자동으로 업데이트하지만 이 옵션을 사용하여 통계를 즉시 업데이트할 수 있습니다.  
  
-   시스템 또는 소프트웨어 문제로 인해 데이터가 손상되지 않았는지 확인하기 위해 데이터베이스 내의 데이터 및 데이터 페이지에 대해 내부 일관성 검사를 수행합니다.  
  
-   데이터베이스 및 트랜잭션 로그 파일을 백업합니다. 데이터베이스 및 로그 백업은 지정된 기간 동안 보존될 수 있습니다. 따라서 데이터베이스를 마지막 데이터베이스 백업 이전 시간으로 복원해야 할 경우 사용될 백업의 기록을 만들 수 있습니다. 차등 백업을 수행할 수도 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 실행합니다. 이는 다양한 동작을 수행하는 작업과 이러한 작업을 실행하도록 하는 유지 관리 계획을 만드는 데 사용할 수 있습니다.  
  
 유지 관리 태스크에 따라 생성된 결과는 텍스트 파일에 보고서로 기록되거나 `sysmaintplan_log`의 유지 관리 계획 테이블(`sysmaintplan_logdetail` 및 `msdb`)에 기록될 수 있습니다. 로그 파일 뷰어에서 이 결과를 보려면 **유지 관리 계획**을 마우스 오른쪽 단추로 클릭하고 **기록 보기**를 클릭합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 유지 관리 계획을 시작하려면 다음 항목을 사용하십시오.  
  
|||  
|-|-|  
|**설명**|**항목**|  
|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 유지 관리 계획을 만드는 방법에 대해 설명합니다.|[유지 관리 계획 만들기](create-a-maintenance-plan.md)|  
|유지 관리 계획 디자인 화면을 사용하여 유지 관리 계획을 만드는 방법에 대해 설명합니다.|[유지 관리 계획 만들기&#40;유지 관리 계획 디자인 화면&#41;](create-a-maintenance-plan-maintenance-plan-design-surface.md)|  
|개체 탐색기에서 사용할 수 있는 유지 관리 계획 기능을 문서화합니다.|[유지 관리 계획 노드&#40;개체 탐색기&#41;](../../ssms/object/object-explorer.md)|  
  
  
