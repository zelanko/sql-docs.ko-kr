---
title: MSSQLSERVER_10531 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e101562fe823ef7339218dc02b30e60027efbcec
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426452"
---
# <a name="mssqlserver10531"></a>MSSQLSERVER_10531
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10531|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_NO_ELIGIBLE_STMT|  
|메시지 텍스트|사용자에게 적절한 권한이 없으므로 캐시에서 계획 지침 '%.*ls'을(를) 만들 수 없습니다. 사용자가 계획 지침을 만들 수 있도록 VIEW SERVER STATE 권한을 부여하십시오.|  
  
## <a name="explanation"></a>설명  
 사용자에게 계획 캐시에서 지정된 계획 지침을 만들 수 있는 적절한 권한이 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 사용자가 계획 지침을 만들 수 있도록 VIEW SERVER STATE 권한을 부여하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [계획 지침](../performance/plan-guides.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
