---
title: sp_repladdcolumn (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repladdcolumn_TSQL
- sp_repladdcolumn
helpviewer_keywords:
- sp_repladdcolumn
ms.assetid: d6220f9f-c738-4f9c-bcf8-419994e86c81
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1b01a48e15c06f021b41b3bded35a0cd2739313c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006920"
---
# <a name="sprepladdcolumn-transact-sql"></a>sp_repladdcolumn(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시된 기존 테이블 아티클에 열을 추가합니다. 이 테이블을 게시하는 모든 게시자에 새 열을 추가하거나 이 테이블을 게시하는 특정 게시에 열을 추가할 수 있습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]
>  이 저장 프로시저는 더 이상 사용되지 않으며 이전 버전과의 호환성을 위해 지원됩니다. 사용 하 여만 사용 해야 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 게시자 및 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 재게시 구독자입니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상에서 도입된 데이터 형식을 사용하는 열에는 이 절차를 사용하지 않아야 합니다.  
  
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
 추가할 새 열을 포함하는 테이블 아티클의 이름입니다. *source_object* 는 **nvarchar (358**), 기본값은 없습니다.  
  
 [ @column =] '*열*'  
 복제용으로 추가될 테이블에 있는 열의 이름입니다. *열* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ @typetext =] '*typetext*'  
 추가되는 열의 정의입니다. *typetext* 됩니다 **nvarchar(3000)** , 기본값은 없습니다. 예를 들어 열 order_filled 추가, 하는 단일 문자 필드에 NULL이 아닌의 기본값이 **N**, order_filled는 것은 *열* 매개 변수를 정의 하는 동안는 열 **char(1) 없습니다 NULL CONSTRAINT constraint_name DEFAULT ' n '** 것은 *typetext* 매개 변수 값입니다.  
  
 [ @publication_to_add =] '*publication_to_add*'  
 새 열을 추가할 게시의 이름입니다. *publication_to_add* 됩니다 **nvarchar(4000)** , 기본값은 **모든**합니다. 하는 경우 **모든**, 다음이 테이블이 포함 된 모든 게시에 영향을 받습니다. 하는 경우 *publication_to_add* 지정 하면이 게시에만 새 열이 추가 됩니다.  
  
 [ @from_agent =] *from_agent*  
 복제 에이전트에서 저장 프로시저를 실행하는 경우 *from_agent* 됩니다 **int**, 기본값은 **0**, 여기서 값 **1** 이 저장된 프로시저를 실행할 때 복제 에이전트에서 사용 됩니다 모든 다른 경우 기본값인 **0**사용 해야 합니다.  
  
 [ @schema_change_script =] '*schema_change_script*'  
 시스템 생성 사용자 지정 저장 프로시저를 수정하는 데 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트의 이름과 경로를 지정합니다. *schema_change_script* 됩니다 **nvarchar(4000)** , 기본값은 NULL입니다. 복제를 사용하면 트랜잭션 복제에서 사용되는 하나 이상의 기본 프로시저를 사용자 정의 사용자 지정 저장 프로시저로 바꿀 수 있습니다. *schema_change_script* 스키마 변경 sp_repladdcolumn을 사용 하 여 복제 된 테이블 아티클에 하려고 하 고 다음 중 하나를 수행할 수 후에 실행 됩니다.  
  
-   사용자 지정 저장된 프로시저는 자동으로 다시 생성 하는 경우 *schema_change_script* 이러한 사용자 지정 저장된 프로시저를 삭제 하 고 그것을 사용자 정의 사용자 지정 저장된 프로시저가 새 스키마를 지 원하는 데 사용할 수 있습니다.  
  
-   사용자 지정 저장된 프로시저는 자동으로 다시 생성 되지 *schema_change_script*이러한 저장된 프로시저를 다시 생성 데 사용할 수 있습니다 또는 저장 프로시저를 사용자 지정 사용자 정의 만듭니다.  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 스냅샷 무효화 기능을 설정하거나 해제합니다. *force_invalidate_snapshot* 되는 **비트**, 기본값은 **1**합니다.  
  
 **1** 지정은 아티클의 변경이을 유효 하지 않게 스냅숏을 무효화 하는 경우, 값 및 **1** 새 스냅숏 발생에 대 한 사용 권한을 부여 합니다.  
  
 **0** 는 아티클에 대 한 변경 인해 스냅숏이 무효화 되지 않도록 지정 합니다.  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 구독 다시 초기화 기능을 설정하거나 해제합니다. *force_reinit_subscription* 되는 **비트** 이며 기본값은 **0**합니다.  
  
 **0** 문서를 변경으로 인해 구독이 다시 초기화 되지 않습니다 지정 합니다.  
  
 **1** 아티클의 변경이 문서 수는 구독이 다시 초기화 되도록 하는 경우, 값 및 **1** 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 고정 서버 역할의 멤버 및 db_owner 고정 데이터베이스 역할의 멤버만 sp_repladdcolumn를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 복제에서 사용 되지 않는 기능](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
