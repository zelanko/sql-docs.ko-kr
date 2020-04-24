---
title: SET CONCAT_NULL_YIELDS_NULL(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONCAT_NULL_YIELDS_NULL_TSQL
- SET CONCAT_NULL_YIELDS_NULL
- CONCAT_NULL_YIELDS_NULL
- SET_CONCAT_NULL_YIELDS_NULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_NULL_YIELDS_NULL option
- null values [SQL Server], concatenation results
- concatenation [SQL Server]
- SET CONCAT_NULL_YIELDS_NULL statement
ms.assetid: 3091b71c-6518-4eb4-88ab-acae49102bc5
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ac123431796331485544b34b15023d34c26a7d6e
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634433"
---
# <a name="set-concat_null_yields_null-transact-sql"></a>SET CONCAT_NULL_YIELDS_NULL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  연결된 결과를 null 값으로 다룰 것인지 또는 빈 문자열 값으로 다룰 것인지를 제어합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 CONCAT_NULL_YIELDS_NULL이 항상 ON으로 설정되어 있으므로 명시적으로 이 옵션을 OFF로 설정한 애플리케이션에서는 오류가 발생합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server  
    
SET CONCAT_NULL_YIELDS_NULL { ON | OFF }   
```  
  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET CONCAT_NULL_YIELDS_NULL ON    
```  
  
## <a name="remarks"></a>설명  
 SET CONCAT_NULL_YIELDS_NULL 옵션이 ON일 경우 NULL 값을 문자열과 연결하면 결과가 NULL 값입니다. 예를 들어 `SELECT 'abc' + NULL`은 `NULL`를 생성합니다. SET CONCAT_NULL_YIELDS_NULL 옵션이 OFF일 경우, NULL 값을 문자열과 연결하면 그 결과가 문자열 자체(NULL 값은 빈 문자열로 처리됨)가 됩니다. 예를 들어 `SELECT 'abc' + NULL`은 `abc`를 생성합니다.  
  
 SET CONCAT_NULL_YIELDS_NULL이 지정되지 않은 경우 **CONCAT_NULL_YIELDS_NULL** 데이터베이스 옵션의 설정이 적용됩니다.  
  
> [!NOTE]  
>  SET CONCAT_NULL_YIELDS_NULL 옵션은 ALTER DATABASE의 CONCAT_NULL_YIELDS_NULL 옵션과 설정이 같습니다.  
  
 SET CONCAT_NULL_YIELDS_NULL 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  

인덱싱된 뷰, 계산 열의 인덱스, 필터링된 인덱스 또는 부분 인덱스를 만들거나 변경할 때는 SET CONCAT_NULL_YIELDS_NULL이 **ON**이어야 합니다. SET CONCAT_NULL_YIELDS_NULL이 **OFF**이면 계산 열의 인덱스, 필터링된 인덱스, 부분 인덱스 또는 인덱싱된 뷰가 있는 테이블에서 CREATE, UPDATE, INSERT, DELETE 문이 실패합니다. 인덱싱된 뷰 및 계산 열의 인덱스에 사용되는 필수 SET 옵션 설정에 대한 자세한 내용은 [SET Statements &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)에서 "SET 문 사용 시 고려 사항"을 참조하세요.
  
 CONCAT_NULL_YIELDS_NULL 옵션을 OFF로 설정하면 서버 경계 간에 문자열을 연결할 수 없습니다.  
  
 이 설정에 대한 현재 설정을 보려면 다음 쿼리를 실행합니다.  
  
```sql
DECLARE @CONCAT_SETTING VARCHAR(3) = 'OFF';  
IF ( (4096 & @@OPTIONS) = 4096 ) SET @CONCAT_SETTING = 'ON';  
SELECT @CONCAT_SETTING AS CONCAT_NULL_YIELDS_NULL; 
```  
  
## <a name="examples"></a>예  
 다음 예에서는 두 `SET CONCAT_NULL_YIELDS_NULL` 설정을 사용하는 방법을 보여 줍니다.  
  
```sql
PRINT 'Setting CONCAT_NULL_YIELDS_NULL ON';  
GO  
-- SET CONCAT_NULL_YIELDS_NULL ON and testing.  
SET CONCAT_NULL_YIELDS_NULL ON;  
GO  
SELECT 'abc' + NULL ;  
GO  
  
-- SET CONCAT_NULL_YIELDS_NULL OFF and testing.  
SET CONCAT_NULL_YIELDS_NULL OFF;  
GO  
SELECT 'abc' + NULL;   
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
