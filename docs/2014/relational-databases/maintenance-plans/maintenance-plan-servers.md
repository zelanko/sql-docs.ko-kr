---
title: 유지 관리 계획(서버) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.maintplanproperties.server.f1
- sql12.swb.maint.servers.f1
ms.assetid: ac24d1a8-dd2f-4162-b804-c0df1fc1e61d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 989b2992407c4a3825d42106d848598a723a41c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63187243"
---
# <a name="maintenance-plan-servers"></a>유지 관리 계획(서버)
  **서버** 대화 상자를 사용하여 유지 관리 계획을 실행할 서버를 선택할 수 있습니다.  
  
 하나의 마스터 서버 및 하나 이상의 대상 서버가 있는 다중 서버 환경은 다중 서버 유지 관리 계획을 만들도록 구성되어야 합니다. 다중 서버 유지 관리 계획의 경우 로컬 서버를 마스터 서버로 구성해야 합니다. 다중 서버 환경에서 이 대화 상자에는 **(로컬)** 마스터 서버와 해당하는 모든 대상 서버가 표시됩니다. 로컬 서버당 하나의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업이 생성되며 이러한 작업은 **(로컬)** 서버의 선택 여부에 따라 수행 또는 수행되지 않습니다. 대상 서버를 선택하면 다중 서버 작업이 생성되고 선택한 각 대상 서버에 다운로드됩니다. 대상 서버를 선택하지 않으면 다중 서버 작업이 삭제됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [유지 관리 계획](maintenance-plans.md)   
 [다중 서버 환경 만들기](../../ssms/agent/create-a-multiserver-environment.md)   
 [마스터 서버 만들기](../../ssms/agent/make-a-master-server.md)   
 [대상 서버 만들기](../../ssms/agent/make-a-target-server.md)  
  
  
