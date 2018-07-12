---
title: MSSQLSERVER_8712 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: db6b162b08fc60a96bda225b1b2118f5644107d2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413762"
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
  
  
