---
title: sp_dropdistpublisher (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistpublisher
- sp_dropdistpublisher_TSQL
helpviewer_keywords:
- sp_dropdistpublisher
ms.assetid: c0bdd3de-3be0-455c-898a-98d4660e7ce3
author: stevestein
ms.author: sstein
ms.openlocfilehash: a15162774d3814e574735d8e1d5fd5e6b769327f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72278121"
---
# <a name="sp_dropdistpublisher-transact-sql"></a>sp_dropdistpublisher(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  배포 게시자를 삭제합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropdistpublisher [ @publisher = ] 'publisher'  
    [ , [ @no_checks = ] no_checks ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`삭제할 게시자입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @no_checks = ] no_checks`게시자가 서버를 배포자로 제거 했는지 여부를 확인 **sp_dropdistpublisher** 여부를 지정 합니다. *no_checks* 은 **bit**이며 기본값은 **0**입니다.  
  
 **0**인 경우 복제는 원격 게시자가 로컬 서버를 배포자로 제거 했는지 확인 합니다. 게시자가 로컬인 경우에는 복제 시 로컬 서버에 게시 또는 배포 개체가 남아 있지 않음을 확인합니다.  
  
 **1**인 경우에는 원격 게시자에 연결할 수 없는 경우에도 배포 게시자와 연결 된 모든 복제 개체가 삭제 됩니다. 이 작업을 수행한 후 원격 게시자는 ** \@ignore_distributor** = **1**과 [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md) 를 사용 하 여 복제를 제거 해야 합니다.  
  
`[ @ignore_distributor = ] ignore_distributor`게시자를 제거할 때 배포 개체가 배포자에 남아 있는지 여부를 지정 합니다. *ignore_distributor* **비트** 이며 다음 값 중 하나일 수 있습니다.  
  
 **1** = *게시자* 에 속하는 배포 개체가 배포자에 남아 있습니다.  
  
 **0** = *게시자* 의 배포 개체가 배포자에서 정리 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropdistpublisher** 은 모든 유형의 복제에 사용 됩니다.  
  
 Oracle 게시자를 삭제할 수 없는 경우에서 **Sp_dropdistpublisher** 게시자를 삭제할 수 없으면 오류가 반환 되 고 게시자의 배포자 개체가 제거 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistpublisher-tra_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_dropdistpublisher**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Transact-sql&#41;sp_adddistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [Transact-sql&#41;sp_changedistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [Transact-sql&#41;sp_helpdistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
