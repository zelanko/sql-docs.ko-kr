---
description: SET FMTONLY(Transact-SQL)
title: SET FMTONLY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FMTONLY_TSQL
- FMTONLY
- SET FMTONLY
- SET_FMTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server], only metadata returned
- SET FMTONLY statement
- FMTONLY option
ms.assetid: 02a1d9ac-2e58-433c-9a07-2c5a4a2214e1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 224611c3af21b85c82b76777b2df54d797eab0e2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465764"
---
# <a name="set-fmtonly-transact-sql"></a>SET FMTONLY(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss-all-md](../../includes/tsql-appliesto-ss-all-md.md)]

  클라이언트에 메타데이터만 반환합니다. 쿼리를 실제로 실행하지 않고 응답 형식을 테스트하는 데 사용할 수 있습니다.  

> [!NOTE]
> 이 기능은 사용할 수 없습니다. 이 기능은 다음 항목으로 대체되었습니다.
>
> - [sp_describe_first_result_set(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)
> - [sp_describe_undeclared_parameters(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)
> - [sys.dm_exec_describe_first_result_set(Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)
> - [sys.dm_exec_describe_first_result_set_for_object(Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
SET FMTONLY { ON | OFF }   
```  

## <a name="remarks"></a>설명

`FMTONLY`가 `ON`인 경우 데이터 행이 없는 행 집합이 열 이름으로 반환됩니다.

Transact-SQL 일괄 처리를 구문 분석할 때 `SET FMTONLY ON`은 아무 효과가 없습니다. 이 효과는 실행 런타임 동안 발생합니다.

기본값은 `OFF`입니다.

## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  

## <a name="examples"></a>예제

다음 Transact-SQL 코드 예제에서는 `FMTONLY`를 `ON`으로 설정합니다. 이 설정으로 인해 SQL Server는 선택한 열에 대한 메타데이터 정보만 반환합니다. 특히 열 이름이 반환됩니다. 데이터 행이 반환되지 않습니다.

이 예제에서 저장 프로시저 `prc_gm29`의 테스트 실행은 다음을 반환합니다.

- 여러 행 집합.
- 해당 `SELECT` 문 중 하나에 있는 여러 테이블의 열입니다.

<!--
Issue 2246 inspired this code example, and the replacement of the two pre-existing examples. 2019/June/03, GM.
-->

```sql
SET NOCOUNT ON;
GO

DROP PROCEDURE IF EXISTS prc_gm29;

DROP TABLE IF EXISTS #tabTemp41;
DROP TABLE IF EXISTS #tabTemp42;
GO

CREATE TABLE #tabTemp41
(
   KeyInt41        INT           NOT NULL,
   Name41          NVARCHAR(16)  NOT NULL,
   TargetDateTime  DATETIME      NOT NULL  DEFAULT GetDate()
);

CREATE TABLE #tabTemp42
(
   KeyInt42 INT          NOT NULL,   -- JOIN-able to KeyInt41.
   Name42   NVARCHAR(16) NOT NULL
);
GO

INSERT INTO #tabTemp41 (KeyInt41, Name41) VALUES (10, 't41-c');
INSERT INTO #tabTemp42 (KeyInt42, Name42) VALUES (10, 't42-p');
GO

CREATE PROCEDURE prc_gm29
AS
BEGIN
SELECT * FROM #tabTemp41;
SELECT * FROM #tabTemp42;

SELECT t41.KeyInt41, t41.TargetDateTime, t41.Name41, t42.Name42
   FROM
                 #tabTemp41 AS t41
      INNER JOIN #tabTemp42 AS t42 on t42.KeyInt42 = t41.KeyInt41
END;
GO

SET DATEFORMAT mdy;

SET FMTONLY ON;
EXECUTE prc_gm29;   -- Returns multiple tables.
SET FMTONLY OFF;
GO

DROP PROCEDURE IF EXISTS prc_gm29;

DROP TABLE IF EXISTS #tabTemp41;
DROP TABLE IF EXISTS #tabTemp42;
GO

/****  Actual Output:
[C:\JunkM\]
>> osql.exe -S myazuresqldb.database.windows.net -U somebody -P secret -d MyDatabase -i C:\JunkM\Issue-2246-a.SQL 

 KeyInt41    Name41           TargetDateTime
 ----------- ---------------- -----------------------

 KeyInt42    Name42
 ----------- ----------------

 KeyInt41    TargetDateTime          Name41           Name42
 ----------- ----------------------- ---------------- ----------------


[C:\JunkM\]
>>
****/
```

## <a name="see-also"></a>관련 항목  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

