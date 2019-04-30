---
title: MSSQL_ENG003724 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f3ea7c8720d43fdba53821091c0664bfe375a57b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191455"
---
# <a name="mssqleng003724"></a>MSSQL_ENG003724
    
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
 데이터베이스 개체를 삭제하기 전에 복제되지 않았는지 확인합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
-   게시 데이터베이스에서 오류가 발생한 경우 개체를 삭제하기 전에 게시에서 해당 아티클을 삭제합니다. 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
-   구독 데이터베이스에서 오류가 발생한 경우 개체를 삭제하기 전에 해당 구독을 삭제합니다. 자세한 내용은 [게시 구독](subscribe-to-publications.md)을 참조하세요. 트랜잭션 게시에 대한 구독의 경우 전체 게시 대신 개별 아티클에 대한 구독을 삭제할 수 있습니다. 자세한 내용은 [sp_procoption&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql)을 참조하세요.  
  
 복제되지 않은 데이터베이스에서 오류가 발생한 경우 [sp_removedbreplication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)을 실행하여 데이터베이스의 개체가 복제된 것으로 표시되지 않도록 하세요.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)  
  
  
