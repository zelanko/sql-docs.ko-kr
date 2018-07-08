---
title: MSSQLSERVER_8649 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6a6d23ff0b9139fab5b85fbdd922d5e3cf18ca3e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410652"
---
# <a name="mssqlserver8649"></a>MSSQLSERVER_8649
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|8649|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|COST_TOO_HIGH|  
|메시지 텍스트|이 쿼리의 예상 비용(%d)이 구성 임계값 %d을(를) 초과하여 쿼리가 취소되었습니다. 시스템 관리자에게 문의하십시오.|  
  
## <a name="explanation"></a>설명  
 쿼리의 예상 비용이 QUERY_GOVERNOR_COST_LIMIT에 설정된 구성 임계값을 초과하여 쿼리가 취소되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
 QUERY_GOVERNOR_COST_LIMIT 옵션을 더 큰 값으로 설정하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SET QUERY_GOVERNOR_COST_LIMIT&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-query-governor-cost-limit-transact-sql)  
  
  
