---
title: PARSENAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PARSENAME_TSQL
- PARSENAME
dev_langs: TSQL
helpviewer_keywords:
- PARSENAME function
- parsing [SQL Server], PARSENAME function
- names [SQL Server], objects
- objects [SQL Server], names
- part of object names [SQL Server]
ms.assetid: abf34f99-9ee9-460b-85b2-930ca5c4b5ae
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 908eb510f3916717065ff7d61f8162b222c1552e
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="parsename-transact-sql"></a>PARSENAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  개체 이름에서 지정된 부분을 반환합니다. 검색 가능한 개체의 부분은 개체 이름, 소유자 이름, 데이터베이스 이름 및 서버 이름입니다.  
  
> [!NOTE]  
>  PARSENAME 함수는 지정된 이름의 개체가 있는지 여부를 나타내지 않으며 지정된 개체 이름에서 지정된 부분만 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
PARSENAME ( 'object_name' , object_piece )   
```  
  
## <a name="arguments"></a>인수  
 '*object_name*'  
 지정된 개체 부분을 검색할 개체의 이름입니다. *object_name* 은 **sysname**합니다. 이 매개 변수는 선택적으로 한정된 개체 이름입니다. 개체 이름의 모든 부분이 정규화된 경우 이 이름은 서버 이름, 데이터베이스 이름, 소유자 이름, 개체 이름의 네 부분으로 이루어질 수 있습니다.  
  
 *object_piece*  
 반환할 개체 부분입니다. *object_piece* 유형의 **int**, 이며 이러한 값을 포함할 수 있습니다.  
  
 1 = 개체 이름  
  
 2 = 스키마 이름  
  
 3 = 데이터베이스 이름  
  
 4 = 서버 이름  
  
## <a name="return-types"></a>반환 형식  
 **nchar**  
  
## <a name="remarks"></a>주의  
 다음 조건 중 하나가 만족되면 PARSENAME이 NULL을 반환합니다.  
  
-   어느 *object_name* 또는 *object_piece* 은 NULL입니다.  
  
-   구문 오류가 발생합니다.  
  
 요청한 개체 부분의 길이가 0 이며 유효 하지 않거나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자입니다. 길이가 0인 개체 이름은 한정된 이름 전체를 올바르지 않은 이름으로 렌더링합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `PARSENAME`을 사용하여 `Person` 데이터베이스의 `AdventureWorks2012` 테이블에 대한 정보를 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 1) AS 'Object Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 2) AS 'Schema Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 3) AS 'Database Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 4) AS 'Server Name';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
Object Name
------------------------------
DimCustomer

(1 row(s) affected)

Schema Name
------------------------------
dbo

(1 row(s) affected)

Database Name
------------------------------
AdventureWorksPDW2012

(1 row(s) affected)

Server Name
------------------------------
(null)

(1 row(s) affected)
```
  
## <a name="see-also"></a>관련 항목:  
 [Quotename&#40; Transact SQL &#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [시스템 함수 &#40; Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

