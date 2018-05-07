---
title: sp_can_tlog_be_applied (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_can_tlog_be_applied_TSQL
- sp_can_tlog_be_applied
dev_langs:
- TSQL
helpviewer_keywords:
- sp_can_tlog_be_applied
ms.assetid: 9c143b6c-27ac-4ab7-98d1-3b7b265f3963
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9c12b7b6147296d753c55a867db007ae6067a135
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spcantlogbeapplied-transact-sql"></a>sp_can_tlog_be_applied(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  트랜잭션 로그 백업을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 적용할 수 있는지 여부를 확인합니다. **sp_can_tlog_be_applied** 데이터베이스가 Restoring 상태에 있어야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_can_tlog_be_applied [ @backup_file_name = ] 'backup_file_name'   
        , [ @database_name = ] 'database_name'   
        , [ @result = ] result OUTPUT  
```  
  
## <a name="arguments"></a>인수  
 [ **@backup_file_name=** ] **'***backup_file_name***'**  
 백업 파일의 이름입니다. *backup_file_name* 은 **nvarchar (128)** 합니다.  
  
 [ **@database_name=** ] **'***database_name***'**  
 데이터베이스의 이름입니다. *database_name*은 **sysname**입니다.  
  
 [  **@result=** ] *결과* **출력**  
 트랜잭션 로그를 데이터베이스에 적용할 수 있는지 여부를 나타냅니다. *결과* 은 **비트**합니다.  
  
 1 = 로그를 적용할 수 있음  
  
 0= 로그를 적용할 수 없음  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_can_tlog_be_applied**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `@MyBitVar` 지역 변수를 선언하여 결과를 저장합니다.  
  
```  
USE master;  
GO  
DECLARE @MyBitVar BIT;  
EXEC sp_can_tlog_be_applied  
     @backup_file_name =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\AdventureWorks2012.bak',  
     @database_name = N'AdventureWorks2012',  
     @result = @MyBitVar OUTPUT;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
