---
description: SET XACT_ABORT(Transact-SQL)
title: SET XACT_ABORT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- XACT_ABORT_TSQL
- XACT_ABORT
- SET XACT_ABORT
- SET_XACT_ABORT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- XACT_ABORT option
- automatic transaction roll backs
- transactions [SQL Server], rolling back
- rolling back transactions, SET XACT_ABORT
- roll back transactions [SQL Server]
- SET XACT_ABORT statement
ms.assetid: cbcaa433-58f2-4dc3-a077-27273bef65b5
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b745de81c42af218c71c1b99e02369fad3feb797
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444645"
---
# <a name="set-xact_abort-transact-sql"></a>SET XACT_ABORT(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

> [!NOTE]
> **THROW** 문은 **SET XACT_ABORT**를 인식합니다. **RAISERROR**는 그렇지 않습니다. 새 애플리케이션에서는 **RAISERROR** 대신 **THROW**를 사용해야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문에서 런타임 오류가 발생할 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 현재 트랜잭션을 자동으로 롤백할 것인지 여부를 지정합니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```syntaxsql
SET XACT_ABORT { ON | OFF }
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명

SET XACT_ABORT 옵션을 ON으로 설정하면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 런타임 오류가 발생할 경우 전체 트랜잭션이 종료된 후 롤백됩니다.

SET XACT_ABORT 옵션을 OFF로 설정하면 일부 경우에 오류를 일으킨 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문만 롤백되고 처리 작업을 계속합니다. SET XACT_ABORT 옵션을 OFF로 설정한 경우에도 오류 심각도에 따라 전체 트랜잭션이 롤백될 수도 있습니다. T-SQL 문의 기본 설정은 OFF지만, 트리거의 기본 설정은 ON입니다.

구문 오류와 같은 컴파일 오류는 SET XACT_ABORT 옵션 설정으로 영향을 받지 않습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 포함한 대부분의 OLE DB 공급자에 대한 암시적 또는 명시적 트랜잭션에서 데이터 수정 문에는 XACT_ABORT 옵션을 ON으로 설정해야 합니다. 공급자가 중첩 트랜잭션을 지원할 경우에만 이 옵션이 필요하지 않습니다.

ANSI_WARNINGS=OFF인 경우 사용 권한 위반으로 인해 트랜잭션이 중단됩니다.

SET XACT_ABORT 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.

이 설정에 대한 현재 설정을 보려면 다음 쿼리를 실행합니다.

```sql
DECLARE @XACT_ABORT VARCHAR(3) = 'OFF';
IF ( (16384 & @@OPTIONS) = 16384 ) SET @XACT_ABORT = 'ON';
SELECT @XACT_ABORT AS XACT_ABORT;

```

## <a name="examples"></a>예제

다음 코드 예에서는 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 있는 트랜잭션에서 외래 키 위반 오류를 일으킵니다. 첫 번째 문 집합에서는 오류가 생성되지만 다른 문이 성공적으로 처리되고 트랜잭션이 성공적으로 커밋됩니다. 두 번째 문 집합에서는 `SET XACT_ABORT` 옵션이 `ON`으로 설정됩니다. 이렇게 설정하면 문 오류로 인해 일괄 처리가 종료되고 트랜잭션이 롤백됩니다.

```sql
IF OBJECT_ID(N't2', N'U') IS NOT NULL
    DROP TABLE t2;
GO
IF OBJECT_ID(N't1', N'U') IS NOT NULL
    DROP TABLE t1;
GO  
CREATE TABLE t1
    (a INT NOT NULL PRIMARY KEY);
CREATE TABLE t2
    (a INT NOT NULL REFERENCES t1(a));
GO
INSERT INTO t1 VALUES (1);
INSERT INTO t1 VALUES (3);
INSERT INTO t1 VALUES (4);
INSERT INTO t1 VALUES (6);
GO
SET XACT_ABORT OFF;
GO
BEGIN TRANSACTION;
INSERT INTO t2 VALUES (1);
INSERT INTO t2 VALUES (2); -- Foreign key error.
INSERT INTO t2 VALUES (3);
COMMIT TRANSACTION;
GO
SET XACT_ABORT ON;
GO
BEGIN TRANSACTION;
INSERT INTO t2 VALUES (4);
INSERT INTO t2 VALUES (5); -- Foreign key error.
INSERT INTO t2 VALUES (6);
COMMIT TRANSACTION;
GO
-- SELECT shows only keys 1 and 3 added.
-- Key 2 insert failed and was rolled back, but
-- XACT_ABORT was OFF and rest of transaction
-- succeeded.
-- Key 5 insert error with XACT_ABORT ON caused
-- all of the second transaction to roll back.
SELECT *
 FROM t2;
GO
```

## <a name="see-also"></a>참고 항목

- [THROW&#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)
- [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)
- [COMMIT TransactION&#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)
- [ROLLBACK TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)
- [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)
- [@@TRANCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
