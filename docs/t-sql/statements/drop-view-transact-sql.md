---
description: DROP VIEW(Transact-SQL)
title: DROP VIEW(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_VIEW_TSQL
- DROP VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- dropping views
- DROP VIEW statement
- deleting views
- indexed views [SQL Server], removing
- views [SQL Server], removing
- removing views
ms.assetid: 03cea355-e39c-46e1-b7db-8832038669dd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e62eecd5132e445f010a7f5804eafdf053bf942b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538136"
---
# <a name="drop-view-transact-sql"></a>DROP VIEW(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스에서 하나 이상의 뷰를 제거합니다. DROP VIEW는 인덱싱된 뷰에 대해 실행할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server, Azure SQL Database, and Azure SQL Data Warehouse
  
DROP VIEW [ IF EXISTS ] [ schema_name . ] view_name [ ...,n ] [ ; ]  
```  
  
```syntaxsql
-- Syntax for Parallel Data Warehouse  
  
DROP VIEW [ schema_name . ] view_name [ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]).|  
  
 이미 있는 경우에만 뷰를 조건부로 삭제합니다.  
  
 *schema_name*  
 뷰가 속한 스키마의 이름입니다.  
  
 *view_name*  
 제거할 뷰의 이름입니다.  
  
## <a name="remarks"></a>설명  
 뷰를 삭제하면 해당 뷰의 정의 및 뷰에 대한 기타 정보가 시스템 카탈로그에서 삭제됩니다. 또한 해당 뷰에 대한 모든 권한도 삭제됩니다.  
  
 DROP TABLE을 사용하여 삭제된 테이블의 뷰는 모두 DROP VIEW를 사용하여 명시적으로 삭제해야 합니다.  
  
 DROP VIEW를 인덱싱된 뷰에 대해 실행하면 뷰의 모든 인덱스가 자동으로 삭제됩니다. 뷰의 모든 인덱스를 표시하려면 [sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)를 사용합니다.  
  
 뷰를 통해 쿼리할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 문에 참조된 모든 데이터베이스 개체가 존재하는지, 문의 컨텍스트 내에서 유효한지, 데이터 변경 문이 데이터 무결성 규칙을 위반하지 않는지 확인합니다. 확인이 실패하면 오류 메시지가 반환됩니다. 성공적으로 확인한 경우 작업이 기본 테이블에 대한 동작으로 변환됩니다. 뷰를 만든 후 원본으로 사용하는 테이블이나 뷰가 변경되었다면 뷰를 삭제한 후 다시 만드는 것이 좋습니다.  
  
 특정 뷰의 종속 관계를 결정하는 방법에 관한 자세한 내용은 [sys.sql_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)를 참조하세요.  
  
 뷰의 텍스트 보기에 대한 자세한 내용은 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 보기에 대한 **CONTROL** 권한, 뷰가 포함된 스키마에 대한 **ALTER** 권한 또는 **db_ddladmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-drop-a-view"></a>A. 뷰 삭제  
 다음 예에서는 `Reorder` 뷰를 제거합니다.  
  
```sql
DROP VIEW IF EXISTS dbo.Reorder ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)   
 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
 
