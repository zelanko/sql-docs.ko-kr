---
title: MSSQLSERVER_8649 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bf9ebea59baa49c921989c75ba24afa12c6f0263
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553158"
---
# <a name="mssqlserver_8649"></a>MSSQLSERVER_8649
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
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
  
## <a name="see-also"></a>참고 항목  
 [SET QUERY_GOVERNOR_COST_LIMIT&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-query-governor-cost-limit-transact-sql)  
  
  
