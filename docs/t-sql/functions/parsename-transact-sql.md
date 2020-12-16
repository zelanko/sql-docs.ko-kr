---
description: PARSENAME(Transact-SQL)
title: PARSENAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PARSENAME_TSQL
- PARSENAME
dev_langs:
- TSQL
helpviewer_keywords:
- PARSENAME function
- parsing [SQL Server], PARSENAME function
- names [SQL Server], objects
- objects [SQL Server], names
- part of object names [SQL Server]
ms.assetid: abf34f99-9ee9-460b-85b2-930ca5c4b5ae
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 02227b388b7c2a50d96aa329fa49c796434f8680
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472024"
---
# <a name="parsename-transact-sql"></a>PARSENAME(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  개체 이름에서 지정된 부분을 반환합니다. 검색 가능한 개체의 부분은 개체 이름, 스키마 이름, 데이터베이스 이름 및 서버 이름입니다. 
  
> [!NOTE]  
>  PARSENAME 함수는 지정된 이름의 개체가 있는지 여부를 나타내지 않으며 지정된 개체 이름에서 지정된 부분만 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql 
PARSENAME ('object_name' , object_piece )
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수

*'object_name'* 지정된 개체 부분을 검색할 개체의 이름을 보관하는 매개 변수입니다. 이 매개 변수는 선택적으로 한정된 개체 이름입니다. 개체 이름의 모든 부분이 정규화된 경우 이 이름은 서버 이름, 데이터베이스 이름, 스키마 이름, 개체 이름의 네 부분으로 이루어질 수 있습니다.  'object_name' 문자열의 각 부분은 nvarchar(128) 또는 256 바이트와 동일한 *sysname* 형식입니다. 문자열에 256바이트를 초과하는 부분이 있는 경우 유효한 sysname이 아니므로 PARSENAME은 해당 부분에 대해 NULL을 반환합니다.
  
*object_piece*  
반환할 개체 부분입니다. *object_piece* 는 **int** 형식이며 다음과 같은 값을 가질 수 있습니다.  
    1 = 개체 이름  
    2 = 스키마 이름  
    3 = 데이터베이스 이름  
    4 = 서버 이름  
  
## <a name="return-type"></a>반환 형식

 **sysname**
  
## <a name="remarks"></a>설명

 다음 조건 중 하나가 만족되면 PARSENAME이 NULL을 반환합니다.  
  
-   *object_name* 또는 *object_piece* 가 NULL입니다.  
  
-   구문 오류가 발생합니다.  
  
 요청한 개체 부분의 길이가 0이고 잘못된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자입니다. 길이가 0인 개체 이름은 한정된 이름 전체를 올바르지 않은 이름으로 렌더링합니다.  
  
## <a name="examples"></a>예제

 다음 예에서는 `PARSENAME`을 사용하여 `Person` 데이터베이스의 `AdventureWorks2012` 테이블에 대한 정보를 반환합니다.  
  
```sql  
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
  
## <a name="see-also"></a>참고 항목

- [QUOTENAME&#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
- [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
- [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
- [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  

