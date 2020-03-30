---
title: MSSQLSERVER_2546 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f43cdb5e07f9ac6d490eabf5f17d194e7446bb49
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68023052"
---
# <a name="mssqlserver_2546"></a>MSSQLSERVER_2546
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
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
  
## <a name="see-also"></a>참고 항목  
[ALTER INDEX&#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[인덱스 다시 구성 및 다시 작성](~/relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
