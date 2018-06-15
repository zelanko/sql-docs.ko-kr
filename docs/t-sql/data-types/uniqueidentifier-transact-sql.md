---
title: uniqueidentifier(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/1/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- uniqueidentifier
- uniqueidentifier_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- globally unique identifiers [SQL Server]
- GUIDs [SQL Server]
ms.assetid: b026035b-f3d2-4d70-989d-3884b4ca0233
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7128398c7ebec1317cb23dede5565c93ed29b169
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33052230"
---
# <a name="uniqueidentifier-transact-sql"></a>uniqueidentifier(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

16바이트 GUID입니다.
  
## <a name="remarks"></a>Remarks  
**uniqueidentifier** 데이터 형식의 열이나 지역 변수는 다음 방법에 따라 값으로 초기화됩니다.
-   [NEWID](../../t-sql/functions/newid-transact-sql.md) 또는 [NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md) 함수를 사용합니다.    
-   문자열 상수에서 *xxxxxxxx*-*xxxx*-*xxxx*-*xxxx*-*xxxxxxxxxxxx* 형식으로 변환합니다. 여기서 *x*는 0-9 또는 a-f 범위의 16진수입니다. 예를 들어 6F9619FF-8B86-D011-B42D-00C04FC964FF는 유효한 **uniqueidentifier** 값입니다.  
  
비교 연산자는 **uniqueidentifier** 값으로 사용할 수 있습니다. 그러나 순서는 두 값의 비트 패턴을 비교하여 구현되지 않습니다. **uniqueidentifier** 값에 대해서는 비교(=, <>, \<, >, \<=, >=) 및 NULL에 대한 확인(IS NULL 및 IS NOT NULL) 연산만 수행할 수 있습니다. 다른 산술 연산자는 사용할 수 없습니다. IDENTITY를 제외한 모든 열 제약 조건과 속성은 **uniqueidentifier** 데이터 형식에서 사용할 수 있습니다.
  
구독이 업데이트되는 병합 복제 및 트랜잭션 복제에서는 **uniqueidentifier** 열을 사용하여 테이블의 여러 복사본에서 행을 고유하게 식별할 수 있습니다.
  
## <a name="converting-uniqueidentifier-data"></a>uniqueidentifier 데이터 변환  
**uniqueidentifier** 형식은 문자 식에서 변환하기 위한 문자 형식으로 간주되므로, 문자 형식으로 변환하기 위한 잘림 규칙이 있습니다. 즉, 문자 식이 다른 크기의 문자 데이터 형식으로 변환되면 새 데이터 형식에 대해 너무 긴 값은 잘립니다. "예" 섹션을 참조하세요.
  
## <a name="limitations-and-restrictions"></a>제한 사항

다음 도구 및 기능은 `uniqueidentifier` 데이터 형식을 지원하지 않습니다.
- PolyBase
- 병렬 데이터 웨어하우스용 [dwloader 로딩 도구](https://msdn.microsoft.com/sql/analytics-platform-system/dwloader)

## <a name="examples"></a>예  
다음 예는 `uniqueidentifier` 값을 `char` 데이터 형식으로 변환합니다.
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
다음 예는 변환될 데이터 형식에서 해당 값이 너무 길면 데이터가 잘림을 보여 줍니다. **uniqueidentifier** 형식은 36자로 제한되므로 길이가 초과된 글자는 잘립니다.
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[NEWID&#40;Transact-SQL&#41;](../../t-sql/functions/newid-transact-sql.md)  
[NEWSEQUENTIALID&#40;Transact-SQL&#41](../../t-sql/functions/newsequentialid-transact-sql.md)    
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)
  
  
