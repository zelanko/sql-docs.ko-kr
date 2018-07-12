---
title: MSSQLSERVER_8689 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85e33cc4231fb4ebf6a3058a20a0257e81a07b6a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37421442"
---
# <a name="mssqlserver8689"></a>MSSQLSERVER_8689
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|8689|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|USEPLAN_ERR_NO_DB|  
|메시지 텍스트|USE PLAN 힌트에 지정된 데이터베이스 '%.*ls'이(가) 없습니다. 기존 데이터베이스를 지정하십시오.|  
  
## <a name="explanation"></a>설명  
 USE PLAN 힌트에 지정된 데이터베이스가 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 USE PLAN 힌트에 지정된 모든 데이터베이스가 있는지 확인하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [계획 지침](../performance/plan-guides.md)  
  
  
