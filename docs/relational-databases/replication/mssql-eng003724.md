---
title: "MSSQL_ENG003724 | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d97300f400557643da18e81201136649d629b681
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng003724"></a>MSSQL_ENG003724
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3724|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|%S_MSG '%.*ls'은(는) 복제에 사용 중이므로 %S_MSG할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 데이터베이스의 개체가 복제되면 **sysarticles** 시스템 테이블(스냅숏 및 트랜잭션 게시의 경우) 또는 **sysmergearticles** 시스템 테이블(병합 게시의 경우)에 복제된 상태로 표시됩니다. 복제된 개체를 삭제하려고 하면 이 오류가 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
 데이터베이스 개체를 삭제하기 전에 복제되지 않았는지 확인합니다. 예를 들어  
  
-   게시 데이터베이스에서 오류가 발생한 경우 개체를 삭제하기 전에 게시에서 해당 아티클을 삭제합니다. 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
-   구독 데이터베이스에서 오류가 발생한 경우 개체를 삭제하기 전에 해당 구독을 삭제합니다. 자세한 내용은 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)을 참조하세요. 트랜잭션 게시에 대한 구독의 경우 전체 게시 대신 개별 아티클에 대한 구독을 삭제할 수 있습니다. 자세한 내용은 [sp_procoption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)을 참조하세요.  
  
 복제되지 않은 데이터베이스에서 오류가 발생한 경우 [sp_removedbreplication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 실행하여 데이터베이스의 개체가 복제된 것으로 표시되지 않도록 하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  

