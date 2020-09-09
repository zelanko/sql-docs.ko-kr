---
description: sp_Removedistpublisherdbreplication(Transact-SQL)
title: sp_removedistpublisherdbreplication (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedistpublisherdbreplication_TSQL
- sp_removedistpublisherdbreplication
helpviewer_keywords:
- sp_removedistpublisherdbreplication
ms.assetid: 9bfe002a-25b5-4226-bcfb-feb2060d6b4a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0a2f8b85702db26764b08b7c62b8db8ff1dda1d0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538603"
---
# <a name="sp_removedistpublisherdbreplication-transact-sql"></a>sp_Removedistpublisherdbreplication(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  배포자의 특정 게시에 속한 게시 메타데이터를 제거합니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_removedistpublisherdbreplication [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 게시자 서버의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_removedistpublisherdbreplication** 는 트랜잭션 및 스냅숏 복제에 사용 됩니다.  
  
 배포 데이터베이스를 삭제 하지 않고 게시 된 데이터베이스를 다시 만들어야 하는 경우에 **sp_removedistpublisherdbreplication** 사용 됩니다. 다음 메타 데이터가 제거됩니다.  
  
-   모든 게시 메타 데이터  
  
-   게시에 속한 모든 아티클의 메타 데이터  
  
-   게시에 대한 모든 구독의 메타 데이터  
  
-   게시에 속한 모든 복제 에이전트 작업의 메타 데이터  
  
## <a name="permissions"></a>사용 권한  
 배포자에서 **sysadmin** 고정 서버 역할의 멤버 또는 배포 데이터베이스에 있는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_removedistpublisherdbreplication**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
