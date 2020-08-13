---
title: sp_droprolemember (Transact-sql) | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1ffff6387f2129c2e3bdb2af726e6b87e665554e
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180106"
---
# <a name="sp_droprolemember-transact-sql"></a>sp_droprolemember(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할에서 보안 계정을 제거합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) 을 사용 하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  

### <a name="syntax-for-both-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에 대 한 구문

```syntaxsql  
sp_droprolemember [ @rolename = ] 'role' ,   
     [ @membername = ] 'security_account'  
```  

### <a name="syntax-for-both-azure-sql-data-warehouse-and-parallel-data-warehouse"></a>Azure SQL Data Warehouse 및 병렬 데이터 웨어하우스의 구문

```syntaxsql  
sp_droprolemember 'role' ,  
     'security_account'  
```  
  
## <a name="arguments"></a>인수  
`[ @rolename = ] 'role'`멤버가 제거 되는 역할의 이름입니다. *role* 은 **sysname**이며 기본값은 없습니다. 현재 데이터베이스에 *역할이* 있어야 합니다.  
  
`[ @membername = ] 'security_account'`역할에서 제거 되는 보안 계정의 이름입니다. *security_account* 는 **sysname**이며 기본값은 없습니다. *security_account* 는 데이터베이스 사용자, 다른 데이터베이스 역할, windows 로그인 또는 windows 그룹이 될 수 있습니다. *security_account* 는 현재 데이터베이스에 있어야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 sp_droprolemember는 sysmembers 테이블에서 행을 삭제하여 데이터베이스 역할의 멤버를 제거합니다. 역할에서 멤버를 제거하는 경우 이 멤버는 해당 역할의 멤버 자격을 통해 부여 받은 모든 사용 권한을 잃게 됩니다.  
  
 고정 서버 역할에서 사용자를 제거하려면 sp_dropsrvrolemember를 사용합니다. public 역할에서는 사용자를 제거할 수 없으며 어떤 역할에서도 dbo는 제거할 수 없습니다.  
  
 Sp_helpuser를 사용 하 여 역할의 멤버를 확인 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 ALTER role을 사용 하 여 역할에 멤버를 추가 합니다.  
  
## <a name="permissions"></a>사용 권한  
 역할에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `JonB` 역할에서 `Sales`라는 사용자를 제거합니다.  
  
```sql
EXEC sp_droprolemember 'Sales', 'Jonb';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `JonB` 역할에서 `Sales`라는 사용자를 제거합니다.  
  
```sql
EXEC sp_droprolemember 'Sales', 'JonB'  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_addrolemember &#40;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [Transact-sql&#41;sp_droprole &#40;](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [Transact-sql&#41;sp_dropsrvrolemember &#40;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [Transact-sql&#41;sp_helpuser &#40;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

