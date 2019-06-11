---
title: sp_droprolemember (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprolemember_TSQL
- sp_droprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprolemember
ms.assetid: c2f19ab1-e742-4d56-ba8e-8ffd40cf4925
ms.author: vanto
author: VanMSFT
manager: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c235c23ac0be8dcaf6dc57dae14be9732f5c09f8
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822446"
---
# <a name="spdroprolemember-transact-sql"></a>sp_droprolemember(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할에서 보안 계정을 제거합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  

### <a name="syntax-for-both-sql-server-and-azure-sql-database"></a>SQL Server와 Azure SQL Database에 대 한 구문

```  
sp_droprolemember [ @rolename = ] 'role' ,   
     [ @membername = ] 'security_account'  
```  

### <a name="syntax-for-both-azure-sql-data-warehouse-and-parallel-data-warehouse"></a>Azure SQL Data Warehouse 및 병렬 데이터 웨어하우스 모두에 대 한 구문

```  
sp_droprolemember 'role' ,  
     'security_account'  
```  
  
## <a name="arguments"></a>인수  
`[ @rolename = ] 'role'` 멤버를 제거 하는 데 사용 되는 역할의 이름이입니다. *역할* 됩니다 **sysname**, 기본값은 없습니다. *역할* 현재 데이터베이스에 존재 해야 합니다.  
  
`[ @membername = ] 'security_account'` 보안 계정 이름의 역할에서 제거 됩니다. *security_account* 됩니다 **sysname**, 기본값은 없습니다. *security_account* 데이터베이스 사용자, 다른 데이터베이스 역할, Windows 로그인 또는 Windows 그룹 일 수 있습니다. *security_account* 현재 데이터베이스에 존재 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 sp_droprolemember는 sysmembers 테이블에서 행을 삭제 하 여 데이터베이스 역할에서 멤버를 제거 합니다. 역할에서 멤버를 제거하는 경우 이 멤버는 해당 역할의 멤버 자격을 통해 부여 받은 모든 사용 권한을 잃게 됩니다.  
  
 고정된 서버 역할에서 사용자를 제거할 sp_dropsrvrolemember를 사용 합니다. 사용자가 public 역할에서 제거할 수 없습니다 및 dbo 역할에서 제거할 수 없습니다.  
  
 Sp_helpuser의 멤버를 확인 하는 데는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할 및 역할에 구성원을 추가 하려면 ALTER ROLE을 사용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 역할에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `JonB` 역할에서 `Sales`라는 사용자를 제거합니다.  
  
```sql
EXEC sp_droprolemember 'Sales', 'Jonb';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `JonB` 역할에서 `Sales`라는 사용자를 제거합니다.  
  
```sql
EXEC sp_droprolemember 'Sales', 'JonB'  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprole&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [sp_dropsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpuser &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

