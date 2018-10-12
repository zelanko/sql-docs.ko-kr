---
title: PRINT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PRINT_TSQL
- PRINT
dev_langs:
- TSQL
helpviewer_keywords:
- PRINT statement
- user-defined messages [SQL Server]
- messages [SQL Server], PRINT statement
- displaying user-defined messages
- viewing user-defined messages
- conditionally returning messages [SQL Server]
ms.assetid: 32ba0729-c4b5-4cfb-a5aa-e8b9402be028
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b713866cc1300f86ed3cdf0786991739e9b002a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705801"
---
# <a name="print-transact-sql"></a>PRINT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  사용자 정의 메시지를 클라이언트에게 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
PRINT msg_str | @local_variable | string_expr  
```  
  
## <a name="arguments"></a>인수  
 *msg_str*  
 문자열 또는 유니코드 문자열 상수입니다. 자세한 내용은 [상수&#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md)을 참조하세요.  
  
 **@** *local_variable*  
 유효한 문자 데이터 형식의 변수입니다. **@**_local\_variable_은 **char**, **nchar**, **varchar** 또는 **nvarchar**이거나 이러한 데이터 형식으로 암시적으로 변환될 수 있어야 합니다.  
  
 *string_expr*  
 문자열을 반환하는 식입니다. 연결된 리터럴 값, 함수 및 변수를 포함할 수 있습니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 메시지 문자열은 비유니코드 문자열일 경우 최대 8,000자까지 가능하며 유니코드 문자열일 경우 최대 4,000자까지 가능합니다. 이보다 긴 문자열은 잘립니다. **varchar(max)** 및 **nvarchar(max)** 데이터 형식은 **varchar(8000)** 및 **nvarchar(4000)** 보다 크지 않은 데이터 형식으로 잘립니다.  
  
 RAISERROR를 사용하여 메시지를 반환할 수도 있습니다. RAISERROR는 PRINT에 비해 3가지 장점이 있습니다.  
  
-   RAISERROR는 C 언어 표준 라이브러리의 printf 함수를 바탕으로 모델링된 메커니즘을 사용하여 인수를 오류 메시지 문자열로 대체할 수 있습니다.  
  
-   RAISERROR는 텍스트 메시지와 별도로 고유 오류 번호, 심각도 및 상태 코드를 지정할 수 있습니다.  
  
-   RAISERROR는 sp_addmessage 시스템 저장 프로시저를 사용하여 생성된 사용자 정의 메시지를 반환하는 데 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-conditionally-executing-print-if-exists"></a>1. 조건에 따라 실행되는 PRINT 문(IF EXISTS)  
 다음 예에서는 `PRINT` 문을 사용하여 조건에 따라 메시지를 반환합니다.  
  
```  
IF @@OPTIONS & 512 <> 0  
    PRINT N'This user has SET NOCOUNT turned ON.';  
ELSE  
    PRINT N'This user has SET NOCOUNT turned OFF.';  
GO  
```  
  
### <a name="b-building-and-displaying-a-string"></a>2. 문자열 만들기 및 표시  
 다음 예에서는 `GETDATE` 함수의 결과를 `nvarchar` 데이터 형식으로 변환하고 `PRINT`에서 반환되도록 리터럴 텍스트와 연결합니다.  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
-- This was required in SQL Server 7.0 or earlier.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-conditionally-executing-print"></a>3. 조건에 따라 실행되는 PRINT 문  
 다음 예에서는 `PRINT` 문을 사용하여 조건에 따라 메시지를 반환합니다.  
  
```  
IF DB_ID() = 1  
    PRINT N'The current database is master.';  
ELSE  
    PRINT N'The current database is not master.';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

