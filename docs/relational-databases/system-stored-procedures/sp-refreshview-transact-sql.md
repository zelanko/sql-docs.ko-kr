---
title: sp_refreshview (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_refreshview
- sp_refreshview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refreshview
ms.assetid: 9ce1d07c-ee66-4a83-8c73-cd2cc104dd08
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f82432aa08e19f0c2174943fd1b2aa3ed9f5c407
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sprefreshview-transact-sql"></a>sp_refreshview(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  비스키마 바운드 뷰에 대한 메타데이터를 업데이트합니다. 뷰가 종속된 기본 개체가 변경되면 뷰의 영구 메타데이터가 최신 상태를 유지하지 못할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_refreshview [ @viewname = ] 'viewname'   
```  
  
## <a name="arguments"></a>인수  
 [  **@viewname=** ] **'***viewname***'**  
 뷰의 이름입니다. *viewname* 은 **nvarchar**, 기본값은 없습니다. *viewname* 다중 부분 식별자가 될 수 있지만 현재 데이터베이스의 뷰만 참조할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 수(실패)  
  
## <a name="remarks"></a>주의  
 보기, schemabinding으로 생성 되지 않는 경우 **sp_refreshview** 보기의 정의 영향을 주는 개체 뷰의 기반이 되며 변경 될 때만 적용 됩니다. 그렇지 않으면 뷰를 쿼리할 때 예기치 않은 결과가 발생할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 뷰에 대한 ALTER 권한이 필요하고 뷰 열이 참조하는 CLR(공용 언어 런타임) 사용자 정의 형식 및 XML 스키마 컬렉션에 대한 REFERENCES 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-updating-the-metadata-of-a-view"></a>1. 뷰의 메타데이터 업데이트  
 다음 예에서는 `Sales.vIndividualCustomer` 뷰의 메타데이터를 새로 고칩니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sp_refreshview N'Sales.vIndividualCustomer';  
```  
  
### <a name="b-creating-a-script-that-updates-all-views-that-have-dependencies-on-a-changed-object"></a>2. 변경한 개체에 대해 종속성이 있는 뷰를 모두 업데이트하는 스크립트 만들기  
 `Person.Person` 테이블이 해당 테이블에서 생성된 모든 뷰의 정의에 영향을 주는 방식으로 변경되었다고 가정합니다. 다음 예에서는 `Person.Person` 테이블에 대해 종속성이 있는 모든 뷰의 메타데이터를 새로 고치는 스크립트를 만듭니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT 'EXEC sp_refreshview ''' + name + ''''   
FROM sys.objects AS so   
INNER JOIN sys.sql_expression_dependencies AS sed   
    ON so.object_id = sed.referencing_id   
WHERE so.type = 'V' AND sed.referenced_id = OBJECT_ID('Person.Person');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_refreshsqlmodule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md)  
  
  
