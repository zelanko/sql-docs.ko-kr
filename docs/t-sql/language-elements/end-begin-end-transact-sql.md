---
description: END(BEGIN...END)(Transact-SQL)
title: END(BEGIN...END)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- END
- END_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- enclosing statements [SQL Server]
- END keyword
- BEGIN...END keyword
- END (BEGIN...END) keyword
ms.assetid: 354c4935-1375-4141-8195-61326662f4d2
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eca6f1267084293f00e5e2b22eabf3a4a15d3c43
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484045"
---
# <a name="end-beginend-transact-sql"></a>END(BEGIN...END)(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  그룹으로 실행되는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 묶습니다. BEGIN...END 블록은 중첩될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
BEGIN   
     { sql_statement | statement_block }   
END   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 { *sql_statement*| *statement_block*}  
 문 블록에 정의된 유효한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이나 문 그룹입니다. 문 블록(일괄 처리)을 정의하려면 흐름 제어 언어 키워드인 BEGIN과 END를 사용합니다. BEGIN...END 블록 내의 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 유효해도 특정 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 동일한 일괄 처리(문 블록) 내에서 그룹화할 수 없습니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서 `BEGIN` 및 `END`는 함께 실행되는 일련의 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 문을 정의합니다. `BEGIN...END` 블록이 포함되지 않은 경우 다음 예제가 연속 반복에 포함됩니다.  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @Iteration INTEGER = 0  
WHILE @Iteration <10  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM dbo.DimCustomer WHERE LastName = 'Adams';  
SET @Iteration += 1  
END;  
```  
  
## <a name="see-also"></a>관련 항목  
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [BEGIN...END &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [흐름 제어 언어 &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [ELSE&#40;IF...ELSE&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/else-if-else-transact-sql.md)   
 [IF...ELSE&#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [WHILE&#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  


