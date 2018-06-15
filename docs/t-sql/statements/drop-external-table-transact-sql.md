---
title: DROP EXTERNAL TABLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02a6a236-0756-4570-abfa-6f677a7df042
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 52a0f615609f3693e7b5e33a8d0e2e5944632d2d
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33699966"
---
# <a name="drop-external-table-transact-sql"></a>DROP EXTERNAL TABLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  다음 위치에서 PolyBase 외부 테이블을 제거합니다. 이때 외부 데이터는 삭제되지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP EXTERNAL TABLE [ database_name . [schema_name ] . | schema_name . ] table_name   
[;]  
```  
  

## <a name="arguments"></a>인수  
 [ *database_name* . [*schema_name*] . | *schema_name* . ] *table_name*  
 제거할 외부 테이블의 한 부분에서 세 부분으로 이루어진 이름입니다. 테이블 이름은 선택적으로 스키마 또는 데이터베이스와 스키마를 포함할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
  
-   테이블이 속한 스키마에 대한 **ALTER** 권한이 필요합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 외부 테이블을 삭제하면 모든 테이블 관련 메타데이터가 제거됩니다. 이때 외부 데이터는 삭제되지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-basic-syntax"></a>1. 기본 구문 사용  
  
```  
DROP EXTERNAL TABLE SalesPerson;  
DROP EXTERNAL TABLE dbo.SalesPerson;  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
### <a name="b-dropping-an-external-table-from-the-current-database"></a>2. 현재 데이터베이스에서 외부 테이블 삭제  
 다음 예제에서는 현재 데이터베이스에서 `ProductVendor1` 테이블, 해당 데이터, 인덱스 및 종속된 뷰를 제거합니다.  
  
```  
DROP EXTERNAL TABLE ProductVendor1;  
```  
  
### <a name="c-dropping-a-table-from-another-database"></a>3. 다른 데이터베이스에서 테이블 삭제  
 다음 예에서는 `EasternDivision` 데이터베이스에서 `SalesPerson` 테이블을 삭제합니다.  
  
```  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  

