---
title: sp_dropdistpublisher (Transact SQL) | Microsoft Docs
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
- sp_dropdistpublisher
- sp_dropdistpublisher_TSQL
helpviewer_keywords:
- sp_dropdistpublisher
ms.assetid: c0bdd3de-3be0-455c-898a-98d4660e7ce3
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bf5001349f38cf69a130d35f57424b8820af61fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spdropdistpublisher-transact-sql"></a>sp_dropdistpublisher(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  배포 게시자를 삭제합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropdistpublisher [ @publisher = ] 'publisher'  
    [ , [ @no_checks = ] no_checks ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publisher=** ] **'***게시자***'**  
 삭제할 게시자입니다. *게시자* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@no_checks=** ] *no_checks*  
 지정 하는지 여부를 **sp_dropdistpublisher** 게시자가 배포자로 서버를 제거 했는지 확인 합니다. *no_checks* 은 **비트**, 기본값은 **0**합니다.  
  
 경우 **0**, 복제 원격 게시자가 배포자로 로컬 서버를 제거 했는지 확인 합니다. 게시자가 로컬인 경우에는 복제 시 로컬 서버에 게시 또는 배포 개체가 남아 있지 않음을 확인합니다.  
  
 경우 **1**, 원격 게시자에 연결할 수 없는 경우에 배포 게시자와 연결 된 모든 복제 개체가 삭제 됩니다. 이 작업을 수행한 후 원격 게시자를 제거 해야 복제를 사용 하 여 [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md) 와 **@ignore_distributor**  =  **1**합니다.  
  
 [  **@ignore_distributor=** ] *ignore_distributor*  
 게시자가 제거될 때 배포자에 배포 개체를 남겨둘지 여부를 지정합니다. *ignore_distributor* 은 **비트** 이며 다음이 값 중 하나일 수 있습니다.  
  
 **1** 에 속하는 배포 개체가 =는 *게시자* 배포자에 남아 있습니다.  
  
 **0** =에 대 한 배포 개체는 *게시자* 정리는 배포자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_dropdistpublisher** 모든 유형의 복제에 사용 됩니다.  
  
 게시자를 삭제할 수 없는 경우 Oracle 게시자를 삭제 하는 경우 **sp_dropdistpublisher** 반환 오류 및 게시자에 대 한 배포자 개체가 제거 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistpublisher-tra_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_dropdistpublisher**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
