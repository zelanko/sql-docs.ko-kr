---
description: sp_addmergealternatepublisher(Transact-SQL)
title: sp_addmergealternatepublisher (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergealternatepublisher_TSQL
- sp_addmergealternatepublisher
helpviewer_keywords:
- sp_addmergealternatepublisher
ms.assetid: de46e0b1-d946-4021-bff6-2d8e3187656d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e0589b82f3126819e1638d90c8e67dea7556aafe
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548366"
---
# <a name="sp_addmergealternatepublisher-transact-sql"></a>sp_addmergealternatepublisher(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  동기화 파트너를 대체하기 위한 구독자 기능을 추가합니다. 게시 속성에서 구독자가 다른 게시자와 동기화할 수 있게 지정해야 합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addmergealternatepublisher [ @publisher= ] 'publisher'  
          , [ @publisher_db= ] 'publisher_db'  
          , [ @publication= ] 'publication'  
          , [ @alternate_publisher= ] 'alternate_synchronization_partner'  
          , [ @alternate_publisher_db= ] 'alternate_publisher_db'  
          , [ @alternate_publication= ] 'alternate_synchronization_partner'  
     , [ @alternate_distributor= ] 'alternate_distributor'   
    [ , [ @friendly_name= ] 'friendly_name' ]   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @alternate_publisher = ] 'alternate_synchronization_partner'` 대체 게시자의 이름입니다. *alternate_synchronization_partner* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @alternate_publisher_db = ] 'alternate_publisher_db'` 대체 게시자에 있는 게시 데이터베이스의 이름입니다. *alternate_publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @alternate_publication = ] 'alternate_synchronization_partner'` 대체 동기화 파트너에 있는 게시의 이름입니다. *alternate_synchronization_partner* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @alternate_distributor = ] 'alternate_distributor'` 대체 동기화 파트너에 대 한 배포자의 이름입니다. *alternate_distributor* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @friendly_name = ] 'friendly_name'` 대체 동기화 파트너를 구성 하는 게시자, 게시 및 배포자의 연결을 식별할 수 있는 표시 이름입니다. *friendly_name* 는 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addmergealternatepublisher** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addmergealternatepublisher**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_dropmergealternatepublisher &#40;](../../relational-databases/system-stored-procedures/sp-dropmergealternatepublisher-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
