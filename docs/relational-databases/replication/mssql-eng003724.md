---
title: MSSQL_ENG003724 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 774d53b8e11e7daefab7c51e0009739d646303ef
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68766670"
---
# <a name="mssqleng003724"></a>MSSQL_ENG003724
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
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
 데이터베이스의 개체가 복제되면 **sysarticles** 시스템 테이블(스냅샷 및 트랜잭션 게시의 경우) 또는 **sysmergearticles** 시스템 테이블(병합 게시의 경우)에 복제된 상태로 표시됩니다. 복제된 개체를 삭제하려고 하면 이 오류가 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
 데이터베이스 개체를 삭제하기 전에 복제되지 않았는지 확인합니다. 예를 들어  
  
-   게시 데이터베이스에서 오류가 발생한 경우 개체를 삭제하기 전에 게시에서 해당 아티클을 삭제합니다. 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
-   구독 데이터베이스에서 오류가 발생한 경우 개체를 삭제하기 전에 해당 구독을 삭제합니다. 자세한 내용은 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)을 참조하세요. 트랜잭션 게시에 대한 구독의 경우 전체 게시 대신 개별 아티클에 대한 구독을 삭제할 수 있습니다. 자세한 내용은 [sp_procoption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)을 참조하세요.  
  
 복제되지 않은 데이터베이스에서 오류가 발생한 경우 [sp_removedbreplication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 실행하여 데이터베이스의 개체가 복제된 것으로 표시되지 않도록 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
