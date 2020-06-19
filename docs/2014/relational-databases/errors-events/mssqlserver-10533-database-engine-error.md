---
title: MSSQLSERVER_10533 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10533 (Database Engine error)
ms.assetid: cc2fbdab-7b90-415f-a1f9-066824344283
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ccef25bc8f594cb6ea0b60aefab838ef27cda6f8
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969793"
---
# <a name="mssqlserver_10533"></a>MSSQLSERVER_10533
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10533|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_NAME_TOO_BIG|  
|메시지 텍스트|계획 지침 이름이 허용된 최대 문자 수인 124자를 초과하므로 계획 지침 '%.*ls'을(를) 만들 수 없습니다. 125자 미만의 이름을 지정하십시오.|  
  
## <a name="explanation"></a>설명  
 계획 지침 이름이 허용된 최대 문자 수인 124자를 초과합니다.  
  
## <a name="user-action"></a>사용자 동작  
 125자 미만의 이름을 지정하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [계획 지침](../performance/plan-guides.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
