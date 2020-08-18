---
description: COL_NAME(Transact-SQL)
title: COL_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COL_NAME
- COL_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- COL_NAME function
- column names [SQL Server]
- names [SQL Server], columns
ms.assetid: 214144ab-f2bc-4052-83cf-caf0a85c4cc6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5e84aa9dca9780bf5f5b10b8fb302ef91115fd91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88311179"
---
# <a name="col_name-transact-sql"></a>COL_NAME(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 함수는 테이블 열의 테이블 ID 번호와 열 ID 번호 값에 따라 해당 테이블 열의 이름을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COL_NAME ( table_id , column_id )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*table_id*  
열이 포함된 테이블의 ID 번호입니다. *table_id* 인수에 **int** 데이터 형식이 있습니다.
  
*column_id*  
열의 ID 번호입니다. *column_id* 인수에 **int** 데이터 형식이 있습니다.
  
## <a name="return-types"></a>반환 형식
**sysname**
  
## <a name="exceptions"></a>예외  
오류가 발생하거나 호출자에게 개체를 볼 수 있는 올바른 권한이 없으면 NULL을 반환합니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자는 소유하고 있거나 권한을 부여받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자에게 개체에 대한 올바른 권한이 없으면 `COL_NAME`와 같은 메타데이터 내보내기 기본 제공 함수에서 NULL을 반환할 수 있습니다. 자세한 내용은 [메타데이터 표시 유형 구성](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.
  
## <a name="remarks"></a>설명  
*table_id* 및 *column_id* 매개 변수는 함께 열 이름 문자열을 생성합니다.
  
테이블 및 열 ID 번호를 얻는 방법에 대한 자세한 내용은 [OBJECT_ID&#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)를 참조하세요.
  
## <a name="examples"></a>예제  
다음 예제에서는 `Employee` 테이블 샘플에서 첫 번째 열 이름을 반환합니다.
  
```sql
-- Uses AdventureWorks  
  
SELECT COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 1) AS FirstColumnName,  
COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 2) AS SecondColumnName;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
ColumnName          
------------   
BusinessEntityID  
```  
  
## <a name="see-also"></a>참고 항목
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COLUMNPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)  
[COL_LENGTH&#40;Transact-SQL&#41;](../../t-sql/functions/col-length-transact-sql.md)
  
  

