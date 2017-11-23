---
title: DROP VIEW (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_VIEW_TSQL
- DROP VIEW
dev_langs: TSQL
helpviewer_keywords:
- dropping views
- DROP VIEW statement
- deleting views
- indexed views [SQL Server], removing
- views [SQL Server], removing
- removing views
ms.assetid: 03cea355-e39c-46e1-b7db-8832038669dd
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4ed2dc16e20179981985cc52812c8dbc44c0624b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-view-transact-sql"></a>DROP VIEW(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스에서 하나 이상의 뷰를 제거합니다. DROP VIEW는 인덱싱된 뷰에 대해 실행할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP VIEW [ IF EXISTS ] [ schema_name . ] view_name [ ...,n ] [ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP VIEW [ schema_name . ] view_name   
[;]  
```  
  
## <a name="arguments"></a>인수  
 *경우에 존재*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]). |  
  
 조건에 따라 이미 있는 경우에 뷰를 삭제 합니다.  
  
 *schema_name*  
 뷰가 속한 스키마의 이름입니다.  
  
 *view_name*  
 제거할 뷰의 이름입니다.  
  
## <a name="remarks"></a>주의  
 뷰를 삭제하면 해당 뷰의 정의 및 뷰에 대한 기타 정보가 시스템 카탈로그에서 삭제됩니다. 또한 해당 뷰에 대한 모든 권한도 삭제됩니다.  
  
 DROP TABLE을 사용하여 삭제된 테이블의 뷰는 모두 DROP VIEW를 사용하여 명시적으로 삭제해야 합니다.  
  
 DROP VIEW를 인덱싱된 뷰에 대해 실행하면 뷰의 모든 인덱스가 자동으로 삭제됩니다. 사용 하 여 모든 인덱스에는 보기에 표시 하려면 [sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)합니다.  
  
 뷰를 통해 쿼리할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 문에 참조된 모든 데이터베이스 개체가 존재하는지, 문의 컨텍스트 내에서 유효한지, 데이터 변경 문이 데이터 무결성 규칙을 위반하지 않는지 확인합니다. 확인이 실패하면 오류 메시지가 반환됩니다. 성공적으로 확인한 경우 작업이 기본 테이블에 대한 동작으로 변환됩니다. 뷰를 만든 후 원본으로 사용하는 테이블이나 뷰가 변경되었다면 뷰를 삭제한 후 다시 만드는 것이 좋습니다.  
  
 특정 뷰의 종속 관계 결정 하는 방법에 대 한 자세한 내용은 참조 [sys.sql_dependencies &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md).  
  
 뷰의 텍스트 보기에 대 한 자세한 내용은 참조 [sp_helptext &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 필요한 **제어** 보기에 대 한 권한이 **ALTER** 뷰 또는 멤버 자격에 포함 된 스키마에 대 한 권한이 **db_ddladmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-drop-a-view"></a>1. 뷰 삭제  
 다음 예에서는 `Reorder` 뷰를 제거합니다.  
  
```  
DROP VIEW dbo.Reorder ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [사용 &#40; Transact SQL &#41;](../../t-sql/language-elements/use-transact-sql.md)   
 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
 
