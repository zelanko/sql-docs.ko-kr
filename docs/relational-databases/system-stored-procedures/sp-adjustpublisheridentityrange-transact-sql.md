---
title: sp_adjustpublisheridentityrange (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adjustpublisheridentityrange_TSQL
- sp_adjustpublisheridentityrange
helpviewer_keywords:
- sp_adjustpublisheridentityrange
ms.assetid: 64f111fd-fb7d-4459-93f7-65f0f8dd7efe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1f58c1a212c722873f66d940de691c89d13d08f5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716299"
---
# <a name="sp_adjustpublisheridentityrange-transact-sql"></a>sp_adjustpublisheridentityrange(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  게시에 대한 ID 범위를 조정하고 게시의 임계값에 기반하여 새 범위를 다시 할당합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_adjustpublisheridentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @table_name = ] 'table_name' ]  
    [ , [ @table_owner= ] 'table_owner' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`새 id 범위가 다시 할당 되는 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @table_name = ] 'table_name'`새 id 범위가 다시 할당 되는 테이블의 이름입니다. *table_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @table_owner = ] 'table_owner'`게시자에 있는 테이블의 소유자입니다. *table_owner* 는 **sysname**이며 기본값은 NULL입니다. *Table_owner* 지정 하지 않으면 현재 사용자의 이름이 사용 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_adjustpublisheridentityrange** 은 모든 유형의 복제에 사용 됩니다.  
  
 자동 ID 범위를 사용할 수 있는 게시인 경우 배포 에이전트 또는 병합 에이전트는 해당 임계값에 기반하여 게시의 ID 범위를 자동으로 조정하는 역할을 합니다. 그러나 어떤 이유로 든 배포 에이전트 또는 병합 에이전트 일정 시간 동안 실행 되지 않고 id 범위 리소스가 임계값 지점에 많이 사용 되는 경우 사용자는 **sp_adjustpublisheridentityrange** 를 호출 하 여 게시자에 대 한 새 값 범위를 할당할 수 있습니다.  
  
 **Sp_adjustpublisheridentityrange**실행 하는 경우 *게시* 또는 *table_name* 를 지정 해야 합니다. 두 가지 모두 지정하거나 둘 다 지정하지 않은 경우 오류가 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_adjustpublisheridentityrange**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Id 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
