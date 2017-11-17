---
title: "고유 식별자 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: d9a995f7d29fe91e14affa9266a9bce73acc9010
ms.openlocfilehash: 1450aa86e3f47ef27be5acd5b5410fe40dd5983e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="uniqueidentifier-transact-sql"></a>uniqueidentifier(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

16바이트 GUID입니다.
  
## <a name="remarks"></a>주의  
열 이나 지역 변수 **uniqueidentifier** 다음과 같은 방법으로 데이터 형식을 값으로 초기화할 수 있습니다.
-   NEWID 함수 사용  
-   형식에서 문자열 상수에서를 변환 하 여 *xxxxxxxx*-*xxxx*-*xxxx*-*xxxx* - *자*, 각 *x* 범위 0-9 또는 a-f에서 16 진수입니다. 예를 들어 6F9619FF-8B86-D011-B42D-00C04FC964FF는 유효한 **uniqueidentifier** 값입니다.  
  
비교 연산자를 함께 사용할 수 있습니다 **uniqueidentifier** 값입니다. 그러나 순서는 두 값의 비트 패턴을 비교하여 구현되지 않습니다. 에 대해 수행할 수 있는 작업만 **uniqueidentifier** 값은 비교 (=, <>, \<, >, \<=, > =) 및 NULL (IS NULL 및 IS NOT NULL) 검사 합니다. 다른 산술 연산자는 사용할 수 없습니다. 모든 열 제약 조건 및 ID 제외 하 고 속성에 사용할 수 있습니다는 **uniqueidentifier** 데이터 형식입니다.
  
병합 복제를 사용 하 여 구독 업데이트가 있는 트랜잭션 복제 **uniqueidentifier** 열 테이블의 여러 복사본에서 행이 고유 하 게 식별 되도록 합니다.
  
## <a name="converting-uniqueidentifier-data"></a>uniqueidentifier 데이터 변환  
**uniqueidentifier** 형식이 문자 형식으로 간주 됩니다는 문자 식에서 변환의 목적에 대 한와 문자 형식으로 변환 하기 위한 잘림 규칙이 이므로 합니다. 즉, 문자 식이 다른 크기의 문자 데이터 형식으로 변환되면 새 데이터 형식에 대해 너무 긴 값은 잘립니다. "예" 섹션을 참조하세요.
  
## <a name="limitations-and-restrictions"></a>제한 사항

이러한 도구와 기능을 지원 하지 않습니다는 `uniqueidentifier` 데이터 형식:
- PolyBase
- [dwloader 로드 도구](https://msdn.microsoft.com/sql/analytics-platform-system/dwloader) 병렬 데이터 웨어하우스에 대 한

## <a name="examples"></a>예  
다음 예는 `uniqueidentifier` 값을 `char` 데이터 형식으로 변환합니다.
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
다음 예는 변환될 데이터 형식에서 해당 값이 너무 길면 데이터가 잘림을 보여 줍니다. 때문에 **uniqueidentifier** 형식은 36 자로 제한, 해당 길이 초과 하는 문자는 잘립니다.
  
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
  
## <a name="see-also"></a>참고 항목
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[NEWID &#40; Transact SQL &#41;](../../t-sql/functions/newid-transact-sql.md)  
[NEWSEQUENTIALID &#40; Transact SQL &#41; ](../../t-sql/functions/newsequentialid-transact-sql.md) 
 [설정 @local_variable &#40; Transact SQL &#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)
  
  

