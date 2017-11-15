---
title: "MSSQLSERVER_5237 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 5237 (Database Engine error)
ms.assetid: 9ff28935-d1eb-47ee-99b3-1a65cb948ce7
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: eafae8fdc25989aaec7ea987d5e72ed7a9221e93
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver5237"></a>MSSQLSERVER_5237
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|5237|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC4_INDEXED_VIEW_CHECK_QUERY_FAILED_NO_ERRORCODE|  
|메시지 텍스트|내부 쿼리 오류로 인해 개체 'NAME'(개체 ID O_ID)에 대한 DBCC 크로스-행 집합 검사에 실패했습니다.|  
  
## <a name="explanation"></a>설명  
DBCC의 내부 오류로 인해 인덱싱된 뷰를 확인하는 쿼리를 실행할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
DBCC 명령을 다시 실행하십시오.  
  
