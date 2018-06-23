---
title: MSSQL_ENG021286 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG021286 error
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
caps.latest.revision: 11
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8135ac1e8062b1985ac1c2d41ee607b8acaa5867
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182006"
---
# <a name="mssqleng021286"></a>MSSQL_ENG021286
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21286|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|충돌 테이블 '%s'이(가) 없습니다.|  
  
## <a name="explanation"></a>설명  
 [sysmergearticles&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysmergearticles-transact-sql)에 나열된 아티클에 대한 충돌 테이블이 실제로는 없는 경우 이 오류가 발생합니다. 병합 복제에 대해 게시된 테이블에서 열을 추가하거나 삭제해도 이 오류가 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 충돌 테이블이 없는 데이터베이스에서 [DBCC CHECKDB&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)를 실행하여 데이터 일관성 문제가 없는지 확인합니다.  
  
 구독자에 충돌 테이블이 없는 경우 해당 구독을 삭제하고 다시 만듭니다. 게시자에 충돌 테이블이 없는 경우 모든 구독을 삭제하고 해당 게시를 삭제한 다음 게시 및 모든 구독을 다시 만듭니다. 자세한 내용은 [데이터 및 데이터베이스 개체 게시](publish/publish-data-and-database-objects.md) 및 [게시 구독](subscribe-to-publications.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)  
  
  
