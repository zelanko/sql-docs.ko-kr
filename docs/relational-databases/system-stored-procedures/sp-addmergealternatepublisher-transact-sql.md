---
title: sp_addmergealternatepublisher (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addmergealternatepublisher_TSQL
- sp_addmergealternatepublisher
helpviewer_keywords:
- sp_addmergealternatepublisher
ms.assetid: de46e0b1-d946-4021-bff6-2d8e3187656d
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cd7c439b29a24c6f1187922a81bbdd3f1acfce0b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spaddmergealternatepublisher-transact-sql"></a>sp_addmergealternatepublisher(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  동기화 파트너를 대체하기 위한 구독자 기능을 추가합니다. 게시 속성에서 구독자가 다른 게시자와 동기화할 수 있게 지정해야 합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@publisher=**] **'***publisher***'**  
 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 게시 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@alternate_publisher=**] **'***alternate_synchronization_partner***'**  
 대체 게시자의 이름입니다. *alternate_synchronization_partner* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@alternate_publisher_db=**] **'***alternate_publisher_db***'**  
 대체 게시자에 있는 게시 데이터베이스의 이름입니다. *alternate_publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@alternate_publication=**] **'***alternate_synchronization_partner***'**  
 대체 동기화 파트너에 있는 게시의 이름입니다. *alternate_synchronization_partner* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@alternate_distributor=**] **'***alternate_distributor***'**  
 대체 동기화 파트너에 대한 배포자의 이름입니다. *alternate_distributor* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@friendly_name=**] **'***friendly_name***'**  
 대체 동기화 파트너를 구성하는 게시자, 게시 및 배포자의 연결을 식별하기 위한 표시 이름입니다. *friendly_name* 은 **nvarchar (255)**, 기본값은 NULL입니다.  
  
 [  **@reserved=**] **'***예약***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_addmergealternatepublisher** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_addmergealternatepublisher**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_dropmergealternatepublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergealternatepublisher-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
