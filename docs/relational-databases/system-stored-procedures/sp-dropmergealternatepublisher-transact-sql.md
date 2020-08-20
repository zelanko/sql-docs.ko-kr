---
description: sp_dropmergealternatepublisher(Transact-SQL)
title: sp_dropmergealternatepublisher (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergealternatepublisher
- sp_dropmergealternatepublisher_TSQL
helpviewer_keywords:
- sp_dropmergealternatepublisher
ms.assetid: a7dee4e2-2a60-41da-9d1d-6f991d7e2c5e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: feaecea81d5d92cfa5fb8e5bf171edc6ea05d99d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481315"
---
# <a name="sp_dropmergealternatepublisher-transact-sql"></a>sp_dropmergealternatepublisher(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  병합 게시에서 대체 게시자를 제거합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergealaternatepublisher [ @publisher = ] 'publisher'    , [ @publisher_db = ] 'publisher_db'    , [ @publication = ] 'publication'    , [ @alternate_publisher = ] 'alternate_publisher'    , [ @alternate_publisher_db = ] 'alternate_publisher_db'    , [ @alternate_publication = ] 'alternate_publication'  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 현재 게시자의 이름입니다. *publisher*는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'` 현재 게시 데이터베이스의 이름입니다. *publisher_db*는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'` 현재 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @alternate_publisher = ] 'alternate_publisher'` 대체 동기화 파트너로 서 삭제할 대체 게시자의 이름입니다. *alternate_publisher*는 **sysname**이며 기본값은 없습니다.  
  
`[ @alternate_publisher_db = ] 'alternate_publisher_db'` 대체 동기화 파트너 게시 데이터베이스로 삭제할 게시 데이터베이스의 이름입니다. *alternate_publisher_db*는 **sysname**이며 기본값은 없습니다.  
  
`[ @alternate_publication = ] 'alternate_publication'` 대체 동기화 파트너 게시로 삭제할 게시의 이름입니다. *alternate_publication*는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropmergealternatepublisher** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_dropmergelternatepublisher**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addmergealternatepublisher &#40;](../../relational-databases/system-stored-procedures/sp-addmergealternatepublisher-transact-sql.md)  
  
  
