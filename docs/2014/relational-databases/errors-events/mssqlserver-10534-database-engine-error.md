---
title: MSSQLSERVER_10534 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10534 (Database Engine error)
ms.assetid: e65bb118-99d5-4fdb-b1d5-0ec70f0a677b
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9814659977492d93b5d2ae330a948d0622eda442
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413502"
---
# <a name="mssqlserver10534"></a>MSSQLSERVER_10534
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10534|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_INVALID_PARAMS|  
|메시지 텍스트|계획 지침 ' %. \*l s에 대 한 지정 된 값 때문에 `@params` 올바르지 않습니다. *parameter_name parameter_type* 형식으로 값을 지정하거나 NULL을 지정하세요.|  
  
## <a name="explanation"></a>설명  
 `@params`에 지정된 값이 잘못되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
 *parameter_name parameter_type* 형식으로 값을 지정하거나 NULL을 지정하세요.  
  
## <a name="see-also"></a>관련 항목  
 [계획 지침](../performance/plan-guides.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
