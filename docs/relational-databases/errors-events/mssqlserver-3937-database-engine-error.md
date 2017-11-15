---
title: "MSSQLSERVER_3937 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 113385d8dd09b70f4d058fb24a113f7065866eeb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|MSSQLSERVER|  
|이벤트 ID|3937|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|XACT_FILESTREAM_ROLLBACK_ERROR|  
|메시지 텍스트|FILESTREAM 필터 드라이버로 트랜잭션이 롤백되었음을 알리는 동안 오류가 발생했습니다. 오류 코드: 0x%0x.|  
  
## <a name="explanation"></a>설명  
트랜잭션에 대한 롤백 알림을 실행하는 동안 RsFx 드라이버에서 오류가 반환되었습니다. 이 오류는 리소스 부족으로 인해 발생한 것 같습니다. 이로 인해 RsFx 필터 드라이버에서 약간의 메모리 누수가 발생할 수 있습니다. 하지만 트랜잭션을 만든 sqlservr.exe 프로세스가 종료되면 이 문제는 해결됩니다.  
  
## <a name="user-action"></a>사용자 동작  
