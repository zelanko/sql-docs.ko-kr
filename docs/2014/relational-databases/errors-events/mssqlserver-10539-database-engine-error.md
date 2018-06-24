---
title: MSSQLSERVER_10539 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 52f90cadcd7f66eebfcc1f722f3a9cc52a1eba1b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081107"
---
# <a name="mssqlserver10539"></a>MSSQLSERVER_10539
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10539|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_NO_PLAN_FOR_STMT|  
|메시지 텍스트|시작 오프셋이 %d인 문에 쿼리 계획을 사용할 수 없으므로 캐시에서 계획 지침 '%.*ls'을(를) 만들 수 없습니다. 이 문제는 아직 만들지 않은 데이터베이스 개체에 문이 종속될 때 발생할 수 있습니다. 필요한 모든 데이터베이스 개체가 있는지 확인하고 계획 지침을 만들기 전에 문을 실행하십시오.|  
  
## <a name="explanation"></a>설명  
 지정한 시작 오프셋을 가진 문에 대한 계획 캐시에서 쿼리 계획을 사용할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 필요한 모든 데이터베이스 개체가 있는지 확인하고 계획 지침을 만들기 전에 문을 실행하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
