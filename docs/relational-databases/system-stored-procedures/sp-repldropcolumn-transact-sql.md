---
title: sp_repldropcolumn (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_repldropcolumn_TSQL
- sp_repldropcolumn
helpviewer_keywords:
- sp_repldropcolumn
ms.assetid: fdc1ec5f-f108-42b4-a2d8-f06a71913ab8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b15bcd0b5a24c464799d1bb8150be59600a85ed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47652891"
---
# <a name="sprepldropcolumn-transact-sql"></a>sp_repldropcolumn(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시된 기존 테이블 아티클에서 열을 삭제합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  이 저장 프로시저는 더 이상 사용되지 않으며 주로 이전 버전과의 호환성을 위해 지원됩니다. 사용 하 여만 사용 해야 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 게시자 및 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 재게시 구독자입니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상에서 도입된 데이터 형식을 사용하는 열에는 이 절차를 사용하지 않아야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_repldropcolumn [ @source_object = ] 'source_object', [ @column = ] 'column'   
    [ , [ @from_agent = ] from_agent]   
    [ , [ @schema_change_script = ] 'schema_change_script' ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>인수  
 [ @source_object =] '*source_object*'  
 삭제할 열을 포함하는 테이블 아티클의 이름입니다. *source_object* 는 nvarchar(258) 이며 기본값은 없습니다.  
  
 [ @column =] '*열*'  
 삭제될 테이블 내에 있는 열의 이름입니다. *열* 는 sysname 이며 기본값은 없습니다.  
  
 [ @from_agent =] *from_agent*  
 복제 에이전트에서 저장 프로시저를 실행하는 경우 *from_agent* 은 int 이며 기본값은 0에서 복제 에이전트가이 저장된 프로시저 실행 되 고 다른 모든 경우의 기본값은 0 사용 해야 하는 경우 값 1은 사용 하는 위치입니다.  
  
 [ @schema_change_script =] '*schema_change_script*'  
 시스템 생성 사용자 지정 저장 프로시저를 수정하는 데 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트의 이름과 경로를 지정합니다. *schema_change_script* 는 nvarchar(4000) 이며 기본값은 NULL입니다. 복제를 사용하면 트랜잭션 복제에서 사용되는 하나 이상의 기본 프로시저를 사용자 정의 사용자 지정 저장 프로시저로 바꿀 수 있습니다. *schema_change_script* 스키마 변경 sp_repldropcolumn을 사용 하 여 복제 된 테이블 아티클에 하려고 하 고 다음 중 하나를 수행할 수 후에 실행 됩니다.  
  
-   사용자 지정 저장된 프로시저는 자동으로 다시 생성 하는 경우 *schema_change_script* 이러한 사용자 지정 저장된 프로시저를 삭제 하 고 그것을 사용자 정의 사용자 지정 저장된 프로시저가 새 스키마를 지 원하는 데 사용할 수 있습니다.  
  
-   사용자 지정 저장된 프로시저는 자동으로 다시 생성 되지 *schema_change_script*이러한 저장된 프로시저를 다시 생성 데 사용할 수 있습니다 또는 저장 프로시저를 사용자 지정 사용자 정의 만듭니다.  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 스냅숏 무효화 기능을 설정하거나 해제합니다. *force_invalidate_snapshot* 는 bit 이며 기본값은 1입니다.  
  
 1은 아티클에 대한 변경으로 인해 스냅숏이 무효화되도록 지정합니다. 또한 해당되는 경우에 한해 값 1은 새 스냅숏을 생성할 수 있도록 권한을 부여합니다.  
  
 0은 아티클에 대한 변경으로 인해 스냅숏이 무효화되지 않도록 지정합니다.  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 구독 다시 초기화 기능을 설정하거나 해제합니다. *force_reinit_subscription* 은 bit 이며 기본값은 0입니다.  
  
 0은 아티클에 대한 변경으로 인해 구독이 다시 초기화되지 않도록 지정합니다.  
  
 1은 아티클에 대한 변경으로 인해 구독이 다시 초기화되도록 지정합니다. 또한 해당되는 경우에 한해 값 1은 구독을 다시 초기화할 수 있도록 권한을 부여합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>사용 권한  
 게시자의 sysadmin 고정 서버 역할 멤버나 게시 데이터베이스의 db_owner 또는 db_ddladmin 고정 데이터베이스 역할 멤버만 sp_repldropcolumn을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 복제에서 사용 되지 않는 기능](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
