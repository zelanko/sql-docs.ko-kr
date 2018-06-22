---
title: MSSQLSERVER_2546 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 41e4f62a27a3f4a126c9d25b00c03f7f4c31b933
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079526"
---
# <a name="mssqlserver2546"></a>MSSQLSERVER_2546
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2546|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_INDEX_MARKED_DISABLED|  
|메시지 텍스트|테이블 'OBJECT_NAME'의 인덱스 'INDEX_NAME'이(가) 비활성화된 것으로 표시되었습니다. 인덱스를 다시 작성하여 온라인 상태로 만드십시오.|  
  
## <a name="explanation"></a>설명  
 지정된 인덱스가 오프라인이거나 비활성화된 것으로 표시되어 검사할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 ALTER INDEX를 사용하여 인덱스를 다시 작성하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [인덱스 다시 구성 및 다시 작성](../indexes/indexes.md)  
  
  
