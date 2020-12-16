---
description: MSSQL_ENG021286
title: MSSQL_ENG021286 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021286 error
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 59066e248bd059376ec26e32d8541a3427366562
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460216"
---
# <a name="mssql_eng021286"></a>MSSQL_ENG021286
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>메시지 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21286|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|충돌 테이블 '%s'이(가) 없습니다.|  
  
## <a name="explanation"></a>설명  
 [sysmergearticles&#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)에 나열된 아티클에 대한 충돌 테이블이 실제로는 없는 경우 이 오류가 발생합니다. 병합 복제에 대해 게시된 테이블에서 열을 추가하거나 삭제해도 이 오류가 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 충돌 테이블이 없는 데이터베이스에서 [DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)를 실행하여 데이터 일관성 문제가 없는지 확인합니다.  
  
 구독자에 충돌 테이블이 없는 경우 해당 구독을 삭제하고 다시 만듭니다. 게시자에 충돌 테이블이 없는 경우 모든 구독을 삭제하고 해당 게시를 삭제한 다음 게시 및 모든 구독을 다시 만듭니다. 자세한 내용은 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md) 및 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
