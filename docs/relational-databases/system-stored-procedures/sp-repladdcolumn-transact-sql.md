---
description: sp_repladdcolumn(Transact-SQL)
title: sp_repladdcolumn (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 48fc4ad0f7881c3afe567d65ee0e0200b59169e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485801"
---
# <a name="sp_repladdcolumn-transact-sql"></a>sp_repladdcolumn(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  게시된 기존 테이블 아티클에 열을 추가합니다. 이 테이블을 게시하는 모든 게시자에 새 열을 추가하거나 이 테이블을 게시하는 특정 게시에 열을 추가할 수 있습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]
>  이 저장 프로시저는 더 이상 사용되지 않으며 이전 버전과의 호환성을 위해 지원됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 게시자 및 재게시 구독자 에서만 사용 해야 합니다 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] . [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상에서 도입된 데이터 형식을 사용하는 열에는 이 절차를 사용하지 않아야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 추가할 새 열을 포함하는 테이블 아티클의 이름입니다. *source_object* 은 **nvarchar (358**) 이며 기본값은 없습니다.  
  
 [ @column =] '*열*'  
 복제용으로 추가될 테이블에 있는 열의 이름입니다. *열* 은 **sysname**이며 기본값은 없습니다.  
  
 [ @typetext = ] '*typetext*'  
 추가되는 열의 정의입니다. *typetext* 는 **nvarchar (3000)** 이며 기본값은 없습니다. 예를 들어 order_filled 열이 추가 되 고 있고이 열이 NULL이 아닌 단일 문자 필드인 경우 기본값 **N이 N**인 경우 order_filled는 *column* 매개 변수이 고, **CHAR (1) NOT NULL 제약 조건 constraint_name default ' N '** 은 *typetext* 매개 변수 값입니다.  
  
 [ @publication_to_add =] '*publication_to_add*'  
 새 열을 추가할 게시의 이름입니다. *publication_to_add* 은 **nvarchar (4000)** 이며 기본값은 **ALL**입니다. **All**인 경우이 테이블을 포함 하는 모든 게시에 영향을 줍니다. *Publication_to_add* 지정 하면이 게시에만 새 열이 추가 됩니다.  
  
 [ @from_agent =] *from_agent*  
 복제 에이전트에서 저장 프로시저를 실행하는 경우 *from_agent* 은 **int**이며 기본값은 **0**입니다. 여기서 값 **1** 은 복제 에이전트가이 저장 프로시저를 실행할 때 사용 되며 다른 모든 경우에는 기본값 **0**을 사용 해야 합니다.  
  
 [ @schema_change_script =] '*schema_change_script*'  
 시스템 생성 사용자 지정 저장 프로시저를 수정하는 데 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트의 이름과 경로를 지정합니다. *schema_change_script* 은 **nvarchar (4000)** 이며 기본값은 NULL입니다. 복제를 사용하면 트랜잭션 복제에서 사용되는 하나 이상의 기본 프로시저를 사용자 정의 사용자 지정 저장 프로시저로 바꿀 수 있습니다. *schema_change_script* 은 sp_repladdcolumn를 사용 하 여 복제 된 테이블 아티클의 스키마를 변경한 후 실행 되며 다음 중 하나를 수행 하는 데 사용할 수 있습니다.  
  
-   사용자 지정 저장 프로시저가 자동으로 다시 생성 되는 경우이 사용자 지정 저장 프로시저를 삭제 하 고 새 스키마를 지 원하는 사용자 정의 사용자 지정 저장 프로시저로 대체 하는 *schema_change_script* 사용할 수 있습니다.  
  
-   사용자 지정 저장 프로시저가 자동으로 다시 생성 되지 않는 경우 이러한 저장 프로시저를 다시 생성 하거나 사용자 정의 사용자 지정 저장 프로시저를 만드는 데 *schema_change_script*사용할 수 있습니다.  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 스냅샷 무효화 기능을 설정하거나 해제합니다. *force_invalidate_snapshot* 은 **bit**이며 기본값은 **1**입니다.  
  
 **1** 은 아티클에 대 한 변경으로 인해 스냅숏이 무효화 되도록 지정 합니다 .이 경우 값 **1** 은 새 스냅숏이 생성 될 수 있는 권한을 부여 합니다.  
  
 **0** 은 아티클에 대 한 변경으로 인해 스냅숏이 무효화 되지 않도록 지정 합니다.  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 구독 다시 초기화 기능을 설정하거나 해제합니다. *force_reinit_subscription* 은 **bit** 이며 기본값은 **0**입니다.  
  
 **0** 은 아티클에 대 한 변경으로 인해 구독이 다시 초기화 되지 않도록 지정 합니다.  
  
 **1** 은 아티클에 대 한 변경으로 인해 구독이 다시 초기화 되도록 지정 합니다 .이 경우 값 **1** 은 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 고정 서버 역할의 멤버 및 db_owner 고정 데이터베이스 역할의 멤버만 sp_repladdcolumn를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 복제에서 사용 되지 않는 기능](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
