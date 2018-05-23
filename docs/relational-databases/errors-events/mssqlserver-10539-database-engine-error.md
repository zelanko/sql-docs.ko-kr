---
title: MSSQLSERVER_10539 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8815d9a7461885d61bc728cd7349aa622b8aaf24
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver10539"></a>MSSQLSERVER_10539
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
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
  
## <a name="see-also"></a>참고 항목  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
