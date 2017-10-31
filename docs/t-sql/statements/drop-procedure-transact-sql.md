---
title: DROP PROCEDURE (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b386dfca28622eb95eec500d909aa7190d081493
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-procedure-transact-sql"></a>DROP PROCEDURE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 현재 데이터베이스에서 하나 이상의 저장 프로시저나 프로시저 그룹을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```tsql  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP { PROC | PROCEDURE } [ IF EXISTS ] { [ schema_name. ] procedure } [ ,...n ]  
```  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP { PROC | PROCEDURE } { [ schema_name. ] procedure_name }  
```  
  
## <a name="arguments"></a>인수  
 *경우에 존재*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 조건에 따라 이미 있는 경우에 프로시저를 삭제 합니다.  
  
 *schema_name*  
 프로시저가 속한 스키마의 이름입니다. 서버 이름이나 데이터베이스 이름을 지정할 수 없습니다.  
  
 *프로시저*  
 제거할 저장 프로시저나 저장 프로시저 그룹의 이름입니다. 번호를 매긴 프로시저 그룹 내의 개별 프로시저는 삭제할 수 없으며 전체 프로시저 그룹이 삭제됩니다.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 저장 프로시저를 제거하기 전에 종속 개체를 확인하여 적절하게 수정합니다. 저장 프로시저를 삭제하고 종속 개체를 업데이트하지 않으면 해당 개체 및 스크립트에서 오류가 발생할 수 있습니다. 자세한 내용은 참조 [저장 프로시저의 종속성 보기](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
## <a name="metadata"></a>메타데이터  
 기존 프로시저의 목록을 표시 하려면 쿼리는 **sys.objects** 카탈로그 뷰에 있습니다. 프로시저 정의 표시 하려면 쿼리는 **sys.sql_modules** 카탈로그 뷰에 있습니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 필요 **제어** 프로시저에 대 한 권한 또는 **ALTER** 에 멤버 자격이 나 해당 프로시저가 속한 스키마에 대 한 권한이 **db_ddladmin** 고정된 서버 역할 .  
  
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
  
 다음 예제에서는 제거 된 `dbo.uspMyProc` 저장 프로시저 되었는데 프로시저가 존재 하지 않는 경우 오류가 발생 하지 않습니다. 이 구문은의 새로운 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다.  
  
```  
DROP PROCEDURE IF EXISTS dbo.uspMyProc;  
GO  
```  
  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [sys.objects &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [저장 프로시저 삭제](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)  
  
  



