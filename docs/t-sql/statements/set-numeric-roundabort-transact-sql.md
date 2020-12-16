---
description: SET NUMERIC_ROUNDABORT(Transact-SQL)
title: SET NUMERIC_ROUNDABORT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NUMERIC_ROUNDABORT
- SET_NUMERIC_ROUNDABORT_TSQL
- SET NUMERIC_ROUNDABORT
- NUMERIC_ROUNDABORT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- rounding expressions
- precision [SQL Server], rounded expressions
- expressions [SQL Server], rounding
- NUMERIC_ROUNDABORT
- SET NUMERIC_ROUNDABORT statement
ms.assetid: d20e74f1-b8da-466c-b180-9d8a8b851a77
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6e8c59df14a87efe967d79d6f2490c9f35f9e76b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471884"
---
# <a name="set-numeric_roundabort-transact-sql"></a>SET NUMERIC_ROUNDABORT(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

식의 반올림에서 정밀도가 손실될 경우 생성되는 오류 보고의 수준을 지정합니다.  
  
![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>구문

```syntaxsql

SET NUMERIC_ROUNDABORT { ON | OFF }
```
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명
SET NUMERIC_ROUNDABORT 옵션을 ON으로 설정하면 식에서 정밀도 손실이 발생할 경우 오류가 생성됩니다. OFF로 설정하면 전체 자릿수가 손실되어도 오류 메시지가 생성되지 않습니다. 결과를 저장하는 열 또는 변수의 전체 자릿수로 결과가 반올림됩니다.  
  
정밀도가 낮은 열이나 변수에 고정 정밀도가 있는 값을 저장하려고 할 때 정밀도 손실이 발생합니다.  
  
SET NUMERIC_ROUNDABORT 옵션을 ON으로 설정하면 SET ARITHABORT 옵션이 생성되는 오류의 심각도를 결정합니다. 다음 표에서는 정밀도 손실이 발생할 때 두 가지 설정의 결과를 보여 줍니다.  
  
|설정|SET NUMERIC_ROUNDABORT ON|SET NUMERIC_ROUNDABORT OFF|
|-------------|--------------------------------|---------------------------------|
|SET ARITHABORT ON|오류가 생성되어 결과 세트가 반환되지 않습니다.|오류나 경고가 생성되지 않고, 결과가 반올림됩니다.|  
|SET ARITHABORT OFF|경고가 반환되고, 식이 NULL을 반환합니다.|오류나 경고가 생성되지 않고, 결과가 반올림됩니다.|  

SET NUMERIC_ROUNDABORT 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.

계산 열이나 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때는 SET NUMERIC_ROUNDABORT 옵션을 OFF로 설정해야 합니다. SET NUMERIC_ROUNDABORT가 ON이면 계산 열 또는 인덱싱된 뷰에 인덱스가 있는 테이블의 다음 명령문이 실패합니다.

- CREATE 
- UPDATE 
- INSERT 
- Delete 

인덱싱된 뷰 및 계산 열의 인덱스에 사용되는 필수 SET 옵션 설정에 대한 자세한 내용은 [SET 문 사용 시 고려 사항](../../t-sql/statements/set-statements-transact-sql.md#considerations-when-you-use-the-set-statements)을 참조하세요.
  
이 설정에 대한 현재 설정을 보려면 다음 쿼리를 실행합니다.
  
```sql
DECLARE @NUMERIC_ROUNDABORT VARCHAR(3) = 'OFF';  
IF ( (8192 & @@OPTIONS) = 8192 ) SET @NUMERIC_ROUNDABORT = 'ON';  
SELECT @NUMERIC_ROUNDABORT AS NUMERIC_ROUNDABORT;  
  
```  
  
## <a name="permissions"></a>사용 권한  
**public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
다음 예제에서는 소수점 네 자리까지 정확한 두 개의 값을 보여줍니다. 소수점 두 자리까지 정확한 변수에 추가 및 저장됩니다. 다음 식에서는 `SET NUMERIC_ROUNDABORT` 설정과 `SET ARITHABORT` 설정을 다르게 지정했을 때의 결과를 보여 줍니다.  
  
```sql
-- SET NOCOUNT to ON,   
-- SET NUMERIC_ROUNDABORT to ON, and SET ARITHABORT to ON.  
SET NOCOUNT ON;  
PRINT 'SET NUMERIC_ROUNDABORT ON';  
PRINT 'SET ARITHABORT ON';  
SET NUMERIC_ROUNDABORT ON;  
SET ARITHABORT ON;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234 ;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
  
-- SET NUMERIC_ROUNDABORT to ON and SET ARITHABORT to OFF.  
PRINT 'SET NUMERIC_ROUNDABORT ON';  
PRINT 'SET ARITHABORT OFF';  
SET NUMERIC_ROUNDABORT ON;  
SET ARITHABORT OFF;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234 ;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
  
-- SET NUMERIC_ROUNDABORT to OFF and SET ARITHABORT to ON.  
PRINT 'SET NUMERIC_ROUNDABORT OFF';  
PRINT 'SET ARITHABORT ON';  
SET NUMERIC_ROUNDABORT OFF;  
SET ARITHABORT ON;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234 ;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
  
-- SET NUMERIC_ROUNDABORT to OFF and SET ARITHABORT to OFF.  
PRINT 'SET NUMERIC_ROUNDABORT OFF';  
PRINT 'SET ARITHABORT OFF';  
SET NUMERIC_ROUNDABORT OFF;  
SET ARITHABORT OFF;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
[SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
[SET ARITHABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)  
  
  
