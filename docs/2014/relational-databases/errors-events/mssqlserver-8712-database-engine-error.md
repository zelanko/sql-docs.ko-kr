---
title: MSSQLSERVER_8712 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b956a9f51e013ce03801ff870e27f337c738b3c6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48202359"
---
# <a name="mssqlserver8712"></a>MSSQLSERVER_8712
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|8712|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|USEPLAN_ERR_NO_INDEX|  
|메시지 텍스트|USE PLAN 힌트에 지정된 인덱스 '%.*ls'이(가) 없습니다. 기존 인덱스를 지정하거나 지정된 이름의 인덱스를 만드십시오.|  
  
## <a name="explanation"></a>설명  
 USE PLAN 힌트에 지정된 인덱스가 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 USE PLAN 힌트에 지정된 모든 인덱스가 있는지 확인하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [계획 지침](../performance/plan-guides.md)  
  
  
