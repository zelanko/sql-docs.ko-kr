---
title: sp_removedistpublisherdbreplication (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: c92355cf5113960d92229157c86346135daad19e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006947"
---
# <a name="spremovedistpublisherdbreplication-transact-sql"></a>sp_Removedistpublisherdbreplication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  배포자의 특정 게시에 속한 게시 메타데이터를 제거합니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_removedistpublisherdbreplication [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 게시자 서버의 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시 데이터베이스의 이름이입니다. *publisher_db* 됩니다 **sysname** 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_removedistpublisherdbreplication** 트랜잭션 및 스냅숏 복제에 사용 됩니다.  
  
 **sp_removedistpublisherdbreplication** 배포 데이터베이스를 삭제 하지 않고 게시 된 데이터베이스를 만들어야 하는 경우에 사용 됩니다. 다음 메타 데이터가 제거됩니다.  
  
-   모든 게시 메타 데이터  
  
-   게시에 속한 모든 아티클의 메타 데이터  
  
-   게시에 대한 모든 구독의 메타 데이터  
  
-   게시에 속한 모든 복제 에이전트 작업의 메타 데이터  
  
## <a name="permissions"></a>사용 권한  
 멤버만 합니다 **sysadmin** 고정된 서버 역할의 멤버나 배포자 합니다 **db_owner** 고정된 데이터베이스 역할의 배포 데이터베이스에서 실행할 수 있습니다 **sp_ removedistpublisherdbreplication**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
