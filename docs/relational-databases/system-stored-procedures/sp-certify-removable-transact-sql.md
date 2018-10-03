---
title: sp_certify_removable (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_certify_removable_TSQL
- sp_certify_removable
dev_langs:
- TSQL
helpviewer_keywords:
- sp_certify_removable
ms.assetid: ca12767f-0ae5-4652-b523-c23473f100a1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1d2586f1ad5f7be9b5916caea7699ca9c90f22db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47691411"
---
# <a name="spcertifyremovable-transact-sql"></a>sp_certify_removable(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이동식 미디어에 배포할 수 있도록 데이터베이스가 제대로 구성되었는지 확인하고 사용자에게 발생한 모든 문제를 보고합니다.  
  
> **중요!!** [!INCLUDE[ssNoteDepFutureAvoid](../../t-sql/statements/create-database-sql-server-transact-sql.md) instead.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_certify_removable [ @dbname= ] 'dbname'  
     [ , [ @autofix = ] 'auto' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@dbname=**] **'***dbname***'**  
 데이터베이스를 확인하도록 지정합니다. *dbname* 됩니다 **sysname**합니다.  
  
 [ **@autofix=**] **'auto'**  
 데이터베이스 및 모든 데이터베이스 개체의 소유권을 시스템 관리자에게 부여하며 사용자가 만든 데이터베이스 사용자 및 기본 권한이 아닌 권한을 모두 삭제합니다. *자동* 됩니다 **nvarchar(4)**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 데이터베이스를 올바르게 구성한 경우 **sp_certify_removable** 다음 작업을 수행 합니다.  
  
-   파일을 복사할 수 있도록 데이터베이스를 오프라인으로 설정합니다.  
  
-   모든 테이블에 있는 통계를 업데이트하며 모든 소유권 및 사용자 문제를 보고합니다.  
  
-   데이터 파일 그룹을 읽기 전용으로 표시하여 해당 파일이 읽기 전용 미디어에만 복사되도록 합니다.  
  
 시스템 관리자는 반드시 데이터베이스 및 모든 데이터베이스 개체의 소유자여야 합니다. 시스템 관리자가 실행 되는 모든 서버에 있는 알려진된 사용자 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 데이터베이스를 나중에 배포 하 고 설치 하는 경우를 예상할 수 있습니다.  
  
 실행 하는 경우 **sp_certify_removable** 없이 **자동** 값과 다음 조건 중 하나에 대 한 정보를 반환 합니다.  
  
-   시스템 관리자가 데이터베이스 소유자가 아닌 경우  
  
-   사용자가 만든 사용자가 있을 경우  
  
-   시스템 관리자가 데이터베이스의 일부 개체를 소유하고 있지 않을 경우  
  
-   기본 권한이 아닌 권한이 부여된 경우  
  
 이러한 경우 다음과 같은 방법으로 문제를 해결할 수 있습니다.  
  
-   사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구 및 프로시저를 실행 한 다음 **sp_certify_removable** 다시 합니다.  
  
-   실행 하기만 **sp_certify_removable** 사용 하 여 합니다 **자동** 값입니다.  
  
 이 저장 프로시저는 사용자 및 사용자 권한에 관한 것만 확인합니다. 데이터베이스에 그룹을 추가하고 이 그룹에 권한을 부여할 수 있습니다. 자세한 내용은 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)과 함께 작동하도록 Service Broker를 구성하는 방법에 대한 정보를 제공합니다.  
  
## <a name="permissions"></a>사용 권한  
 실행 권한은의 멤버로 제한 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `inventory` 데이터베이스를 제거할 준비가 되었음을 증명합니다.  
  
```  
EXEC sp_certify_removable inventory, AUTO;  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_create_removable &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-removable-transact-sql.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
