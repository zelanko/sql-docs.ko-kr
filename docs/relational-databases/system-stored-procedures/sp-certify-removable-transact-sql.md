---
description: sp_certify_removable(Transact-SQL)
title: sp_certify_removable (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5c80828117bfa4219d6f7377c4ed0123dec977aa
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753530"
---
# <a name="sp_certify_removable-transact-sql"></a>sp_certify_removable(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이동식 미디어에 배포할 수 있도록 데이터베이스가 제대로 구성되었는지 확인하고 사용자에게 발생한 모든 문제를 보고합니다.  
  
> **중요!!** [! 대신[ssnotedepfutureavoid&lt](../../t-sql/statements/create-database-transact-sql.md) 를 포함 합니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_certify_removable [ @dbname= ] 'dbname'  
     [ , [ @autofix = ] 'auto' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @dbname = ] 'dbname'` 확인할 데이터베이스를 지정 합니다. *dbname* 은 **sysname**입니다.  
  
`[ @autofix = ] 'auto'` 는 데이터베이스 및 모든 데이터베이스 개체의 소유권을 시스템 관리자에 게 제공 하 고 사용자가 만든 데이터베이스 사용자 및 기본 권한이 아닌 권한을 모두 삭제 합니다. *auto* 는 **nvarchar (4)** 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 데이터베이스가 올바르게 구성 된 경우 **sp_certify_removable** 다음을 수행 합니다.  
  
-   파일을 복사할 수 있도록 데이터베이스를 오프라인으로 설정합니다.  
  
-   모든 테이블에 있는 통계를 업데이트하며 모든 소유권 및 사용자 문제를 보고합니다.  
  
-   데이터 파일 그룹을 읽기 전용으로 표시하여 해당 파일이 읽기 전용 미디어에만 복사되도록 합니다.  
  
 시스템 관리자는 반드시 데이터베이스 및 모든 데이터베이스 개체의 소유자여야 합니다. 시스템 관리자는를 실행 하는 모든 서버에 존재 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하며 나중에 데이터베이스를 배포 하 고 설치할 때 존재 하는 것으로 예상할 수 있는 알려진 사용자입니다.  
  
 **Auto** 값 없이 **sp_certify_removable** 를 실행 하는 경우 다음 조건에 대 한 정보를 반환 합니다.  
  
-   시스템 관리자가 데이터베이스 소유자가 아닌 경우  
  
-   사용자가 만든 사용자가 있을 경우  
  
-   시스템 관리자가 데이터베이스의 일부 개체를 소유하고 있지 않을 경우  
  
-   기본 권한이 아닌 권한이 부여된 경우  
  
 이러한 경우 다음과 같은 방법으로 문제를 해결할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]도구 및 절차를 사용 하 고 **sp_certify_removable** 를 다시 실행 합니다.  
  
-   **Auto** 값을 사용 하 여 **sp_certify_removable** 를 실행 하면 됩니다.  
  
 이 저장 프로시저는 사용자 및 사용자 권한에 관한 것만 확인합니다. 데이터베이스에 그룹을 추가하고 이 그룹에 권한을 부여할 수 있습니다. 자세한 내용은 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)과 함께 작동하도록 Service Broker를 구성하는 방법에 대한 정보를 제공합니다.  
  
## <a name="permissions"></a>사용 권한  
 Execute 권한은 **sysadmin** 고정 서버 역할의 멤버로 제한 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `inventory` 데이터베이스를 제거할 준비가 되었음을 증명합니다.  
  
```  
EXEC sp_certify_removable inventory, AUTO;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Transact-sql&#41;sp_create_removable &#40;](../../relational-databases/system-stored-procedures/sp-create-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Transact-sql&#41;sp_dbremove &#40;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
