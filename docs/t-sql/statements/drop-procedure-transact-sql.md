---
title: DROP PROCEDURE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP PROCEDURE
- DROP_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing stored procedures
- dropping procedure groups
- deleting stored procedures
- deleting procedure groups
- DROP PROCEDURE statement
- dropping stored procedures
- stored procedures [SQL Server], removing
- removing procedure groups
ms.assetid: 1c2d7235-7b9b-4336-8f17-429e7d82c2c3
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c97f61aa00ba7242f6d02920fda91949adbff1c6
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484128"
---
# <a name="drop-procedure-transact-sql"></a>DROP PROCEDURE(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 현재 데이터베이스에서 하나 이상의 저장 프로시저나 프로시저 그룹을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
DROP { PROC | PROCEDURE } [ IF EXISTS ] { [ schema_name. ] procedure } [ ,...n ]  
```  
  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP { PROC | PROCEDURE } { [ schema_name. ] procedure_name }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 이미 있는 경우에만 프로시저를 조건부로 삭제합니다.  
  
 *schema_name*  
 프로시저가 속한 스키마의 이름입니다. 서버 이름이나 데이터베이스 이름을 지정할 수 없습니다.  
  
 *procedure*  
 제거할 저장 프로시저나 저장 프로시저 그룹의 이름입니다. 번호를 매긴 프로시저 그룹 내의 개별 프로시저는 삭제할 수 없으며 전체 프로시저 그룹이 삭제됩니다.  
  
## <a name="best-practices"></a>모범 사례  
 저장 프로시저를 제거하기 전에 종속 개체를 확인하여 적절하게 수정합니다. 저장 프로시저를 삭제하고 종속 개체를 업데이트하지 않으면 해당 개체 및 스크립트에서 오류가 발생할 수 있습니다. 자세한 내용은 [저장 프로시저의 종속성 보기](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)를 참조하세요.  
  
## <a name="metadata"></a>메타데이터  
 기존 프로시저 목록을 표시하려면 **sys.objects** 카탈로그 뷰를 쿼리하세요. 프로시저 정의를 표시하려면 **sys.sql_modules** 카탈로그 뷰를 쿼리하세요.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 프로시저에 대한 **CONTROL** 권한, 프로시저가 속한 스키마에 대한 **ALTER** 권한 또는 **db_ddladmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 데이터베이스의 `dbo.uspMyProc` 저장 프로시저를 제거합니다.  
  
```  
DROP PROCEDURE dbo.uspMyProc;  
GO  
```  
  
 다음 예에서는 현재 데이터베이스의 여러 저장 프로시저를 제거합니다.  
  
```  
DROP PROCEDURE dbo.uspGetSalesbyMonth, dbo.uspUpdateSalesQuotes, dbo.uspGetSalesByYear;  
```  
  
 다음 예제에서는 프로시저가 존재하지만 해당 프로시저가 없어도 오류가 발생하지 않으면 현재 데이터베이스에서 `dbo.uspMyProc` 저장 프로시저를 제거합니다. 이 구문은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 새로운 구문입니다.  
  
```  
DROP PROCEDURE IF EXISTS dbo.uspMyProc;  
GO  
```  
  
  
## <a name="see-also"></a>참고 항목  
 [ALTER PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [저장 프로시저 삭제](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)  
  
  


