---
title: MSSQLSERVER_2530 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: 5d4be07a-38a5-4b25-819c-4dcb4636cc15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8058c7c31c49935d244726bf9e8ea0ac6cfbe750
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62914574"
---
# <a name="mssqlserver_2530"></a>MSSQLSERVER_2530
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2530|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_INDEX_IS_OFFLINE|  
|메시지 텍스트|테이블 "%.\*ls"의 인덱스 "%.*ls"이(가) 비활성화되었습니다.|  
  
## <a name="explanation"></a>설명  
 지정된 인덱스가 비활성화되어 있으므로 DBCC 문을 계속 실행할 수 없습니다. 인덱스는 비활성화되면 다시 작성되거나 삭제 및 다시 생성될 때까지 비활성화된 상태로 유지됩니다.  
  
## <a name="user-action"></a>사용자 동작  
  
1.  다음 중 한 가지 방법을 사용하여 비활성화된 인덱스를 활성화합니다.  
  
    -   REBUILD 절과 함께 ALTER INDEX 문  
  
    -   DROP_EXISTING 절과 함께 CREATE INDEX  
  
    -   DBCC DBREINDEX  
  
2.  해당 DBCC 문을 다시 실행하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [인덱스 및 제약 조건 사용](../indexes/enable-indexes-and-constraints.md)   
 [ALTER INDEX &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [CREATE INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [DBCC DBREINDEX&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)  
  
  
