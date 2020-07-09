---
title: MSSQLSERVER_8649 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d305866fb884b62540cfbe2cc13a613981999749
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765282"
---
# <a name="mssqlserver_8649"></a>MSSQLSERVER_8649
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
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
[SET QUERY_GOVERNOR_COST_LIMIT&#40;Transact-SQL&#41;](~/t-sql/statements/set-query-governor-cost-limit-transact-sql.md)  
  
