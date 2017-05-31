---
title: "MSSQLSERVER_8710 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8b4444dc2ed1b239670c75321ec3a0e1401122a0
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver8710"></a>MSSQLSERVER_8710
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|MSSQLSERVER|  
|이벤트 ID|8710|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|QUERY2_CUBE_ILLEGAL_AGG_FUNC|  
|메시지 텍스트|CUBE, ROLLUP 또는 GROUPING SET 쿼리에 사용되는 집계 함수는 하위 집계 병합을 지원해야 합니다. 이 문제를 해결하려면 집계 함수를 제거하거나 GROUP BY 절 대신 UNION ALL을 사용하여 쿼리를 작성하십시오.|  
  
## <a name="explanation"></a>설명  
하위 집계 병합 방법을 제공하지 않는 CUBE, ROLLUP 또는 GROUPING SETS에 집계 함수가 사용되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
이 문제를 해결하려면 집계 함수를 제거하거나 GROUP BY 절 대신 UNION ALL을 사용하여 쿼리를 작성하십시오.  
  

