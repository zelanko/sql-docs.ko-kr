---
title: sp_repladdcolumn (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_repladdcolumn_TSQL
- sp_repladdcolumn
helpviewer_keywords:
- sp_repladdcolumn
ms.assetid: d6220f9f-c738-4f9c-bcf8-419994e86c81
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d638619d087d43b0820fdf21650a9b8db1f7cf63
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sprepladdcolumn-transact-sql"></a>sp_repladdcolumn(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시된 기존 테이블 아티클에 열을 추가합니다. 이 테이블을 게시하는 모든 게시자에 새 열을 추가하거나 이 테이블을 게시하는 특정 게시에 열을 추가할 수 있습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  이 저장 프로시저는 더 이상 사용되지 않으며 이전 버전과의 호환성을 위해 지원됩니다. 와 사용 해야 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 게시자 및 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 구독자를 다시 게시 합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상에서 도입된 데이터 형식을 사용하는 열에는 이 절차를 사용하지 않아야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_repladdcolumn [ @source_object = ] 'source_object', [ @column = ] 'column' ]  
    [ , [ @typetext = ] 'typetext' ]  
    [ , [ @publication_to_add = ] 'publication_to_add' ]  
    [ , [ @from_agent = ] from_agent ]  
    [ , [ @schema_change_script = ] 'schema_change_script' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>인수  
 [ @source_object =] '*source_object*'  
 추가할 새 열을 포함하는 테이블 아티클의 이름입니다. *source_object* 은 **nvarchar (358**), 기본값은 없습니다.  
  
 [ @column =] '*열*'  
 복제용으로 추가될 테이블에 있는 열의 이름입니다. *열* 은 **sysname**, 기본값은 없습니다.  
  
 [ @typetext =] '*typetext*'  
 추가되는 열의 정의입니다. *typetext* 은 **nvarchar (3000)**, 기본값은 없습니다. 예를 들어, 단일 문자 필드 not NULL 이며 기본 값이 더 order_filled 열을 추가 하는 경우 **N**, 되며는 *열* 정의 하는 동안 매개 변수는 열에서 **char(1) 하지 NULL CONSTRAINT constraint_name DEFAULT ' n '** 것은 *typetext* 매개 변수 값입니다.  
  
 [ @publication_to_add =] '*publication_to_add*'  
 새 열을 추가할 게시의 이름입니다. *publication_to_add* 은 **nvarchar (4000)**, 기본값은 **모든**합니다. 경우 **모든**, 다음이 테이블이 포함 된 모든 게시에 적용 됩니다. 경우 *publication_to_add* 를 지정 하면이 게시에만 새 열이 추가 됩니다.  
  
 [ @from_agent =] *from_agent*  
 복제 에이전트에서 저장 프로시저를 실행하는 경우 *from_agent* 은 **int**, 기본값은 **0**여기서 값, **1** 및 복제 에이전트가이 저장된 프로시저를 실행할 때 사용 됩니다 다른 모든 경우의 기본값 **0**사용 해야 합니다.  
  
 [ @schema_change_script =] '*schema_change_script*'  
 시스템 생성 사용자 지정 저장 프로시저를 수정하는 데 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트의 이름과 경로를 지정합니다. *schema_change_script* 은 **nvarchar (4000)**, 기본값은 NULL입니다. 복제를 사용하면 트랜잭션 복제에서 사용되는 하나 이상의 기본 프로시저를 사용자 정의 사용자 지정 저장 프로시저로 바꿀 수 있습니다. *schema_change_script* 스키마 변경 복제 된 테이블 아티클에 sp_repladdcolumn을 사용 하 여 하 고 다음 중 하나를 수행 하는 데 사용 될 후 실행 됩니다.  
  
-   사용자 지정 저장된 프로시저는 자동으로 다시 생성, *schema_change_script* 이러한 사용자 지정 저장된 프로시저를 삭제 하 고 그것을 사용자 정의 사용자 지정 저장된 프로시저를 새 스키마를 지 원하는 데 사용할 수 있습니다.  
  
-   사용자 지정 저장된 프로시저는 자동으로 다시 생성 되지 *schema_change_script*이러한 저장된 프로시저를 다시 생성 하는 데 사용 될 또는 저장 프로시저를 만들려면 사용자 정의 사용자 지정 합니다.  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 스냅숏 무효화 기능을 설정하거나 해제합니다. *force_invalidate_snapshot* 는 **비트**, 기본값은 **1**합니다.  
  
 **1** 변경이 유효 하려면 스냅숏을 무효화 하 지정 되는 경우에는 값의 경우 **1** 새 스냅숏 발생에 대 한 사용 권한을 부여 합니다.  
  
 **0** 은 아티클의 변경이 스냅숏을 무효화 인해 되지 않도록 지정 합니다.  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 구독 다시 초기화 기능을 설정하거나 해제합니다. *force_reinit_subscription* 는 **비트** 기본값인 **0**합니다.  
  
 **0** 문서에 대 한 변경으로 인해 구독이 다시 초기화 해야 하지 않도록 지정 합니다.  
  
 **1** 아티클의 문서에 대 한 변경 될 수 있습니다는 구독이 다시 초기화 되도록 해당 되는 경우의 값 및 **1** 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>Permissions  
 sysadmin 고정 서버 역할의 멤버 및 db_owner 고정 데이터베이스 역할의 멤버만 sp_repladdcolumn를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 복제에 사용 되지 않는 기능](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
