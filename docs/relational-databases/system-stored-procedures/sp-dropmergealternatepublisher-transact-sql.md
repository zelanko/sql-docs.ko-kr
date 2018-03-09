---
title: sp_dropmergealternatepublisher (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_dropmergealternatepublisher
- sp_dropmergealternatepublisher_TSQL
helpviewer_keywords: sp_dropmergealternatepublisher
ms.assetid: a7dee4e2-2a60-41da-9d1d-6f991d7e2c5e
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4eee448c0fa45270d492f3bf664016ffb2c4dd0d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spdropmergealternatepublisher-transact-sql"></a>sp_dropmergealternatepublisher(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 게시에서 대체 게시자를 제거합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergealaternatepublisher [ @publisher = ] 'publisher'    , [ @publisher_db = ] 'publisher_db'    , [ @publication = ] 'publication'    , [ @alternate_publisher = ] 'alternate_publisher'    , [ @alternate_publisher_db = ] 'alternate_publisher_db'    , [ @alternate_publication = ] 'alternate_publication'  
```  
  
## <a name="arguments"></a>인수  
 [  **@publisher=**] **'***게시자***'**  
 현재 게시자의 이름입니다. *게시자*은 **sysname**, 기본값은 없습니다.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 현재 게시 데이터베이스의 이름입니다. *publisher_db*은 **sysname**, 기본값은 없습니다.  
  
 [  **@publication =**] **'***게시***'**  
 현재 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@alternate_publisher=**] **'***alternate_publisher***'**  
 대체 동기화 파트너로서 삭제할 대체 게시자의 이름입니다. *alternate_publisher*은 **sysname**, 기본값은 없습니다.  
  
 [  **@alternate_publisher_db=**] **'***alternate_publisher_db***'**  
 대체 동기화 파트너 게시 데이터베이스로서 삭제할 게시 데이터베이스의 이름입니다. *alternate_publisher_db*은 **sysname**, 기본값은 없습니다.  
  
 [  **@alternate_publication=**] **'***alternate_publication***'**  
 대체 동기화 파트너 게시로서 삭제할 게시의 이름입니다. *alternate_publication*은 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_dropmergealternatepublisher** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_dropmergelternatepublisher**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_addmergealternatepublisher &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergealternatepublisher-transact-sql.md)  
  
  
