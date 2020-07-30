---
title: SET ANSI_DEFAULTS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET ANSI_DEFAULTS
- ANSI_DEFAULTS
- SET_ANSI_DEFAULTS_TSQL
- ANSI_DEFAULTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ANSI_DEFAULTS option
- SET ANSI_DEFAULTS statement
ms.assetid: bd721d97-6e23-488b-8c8c-c0453d5b3b86
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 087fc2be7400052c2bbd3e82999c66b052422f99
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394708"
---
# <a name="set-ansi_defaults-transact-sql"></a>SET ANSI_DEFAULTS(Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  몇몇 ISO 표준 동작을 전체적으로 지정하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 그룹을 제어합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>구문

```syntaxsql
-- Syntax for SQL Server

SET ANSI_DEFAULTS { ON | OFF }
```

```syntaxsql
-- Syntax for Azure Synapse and Parallel Data Warehouse

SET ANSI_DEFAULTS ON
```

## <a name="remarks"></a>설명  
ANSI_DEFAULTS는 모든 클라이언트 연결의 동작을 사용하도록 설정할 수 있는 서버 측 설정입니다. 클라이언트는 일반적으로 연결 시점에 또는 세션 초기화 시점에 이 설정을 요청합니다. 사용자가 서버 설정을 수정하면 안 됩니다.   
사용자가 클라이언트 동작을 변경하려면 `SQL_COPT_SS_PRESERVE_CURSORS`와 같은 특정 메서드를 사용해야 합니다. 자세한 내용은 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)을 참조하세요.
  
이 옵션이 설정(ON)되어 있는 경우 다음 ISO 설정을 사용할 수 있습니다.  
  
:::row:::
    :::column:::
        SET ANSI_NULLS
    :::column-end:::
    :::column:::
        SET CURSOR_CLOSE_ON_COMMIT
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        SET ANSI_NULL_DFLT_ON
    :::column-end:::
    :::column:::
        SET IMPLICIT_TRANSACTIONS
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        SET ANSI_PADDING
    :::column-end:::
    :::column:::
        SET QUOTED_IDENTIFIER
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        SET ANSI_WARNINGS
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

&nbsp;

또한 이러한 ISO 표준 SET 옵션은 사용자 작업 세션 기간, 실행 중인 트리거, 저장 프로시저에 대해 쿼리 처리 환경을 정의합니다. 하지만 이러한 SET 옵션에는 ISO 표준을 따르는 데 필요한 모든 옵션이 포함되어 있지 않습니다.  
  
계산 열이나 인덱싱된 뷰의 인덱스를 처리할 때 네 가지 기본값(`ANSI_NULLS`, `ANSI_PADDING`, `ANSI_WARNINGS`, `QUOTED_IDENTIFIER`)을 ON으로 설정해야 합니다. 이 기본값은 계산 열과 인덱싱된 뷰에서 인덱스를 만들고 변경할 때 필요한 값이 할당되어야 할 7가지 SET 옵션에 포함됩니다. 나머지 SET 옵션은 `ARITHABORT`(ON), `CONCAT_NULL_YIELDS_NULL`(ON), `NUMERIC_ROUNDABORT`(OFF)입니다. 인덱싱된 뷰 및 계산 열의 인덱스가 있는 필수 SET 옵션 설정에 대한 자세한 내용은 [SET 문 사용 시 고려 사항](../../t-sql/statements/set-statements-transact-sql.md#considerations-when-you-use-the-set-statements)을 참조하세요.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 연결될 때 자동으로 ANSI_DEFAULTS를 ON으로 설정합니다. 그런 다음 CURSOR_CLOSE_ON_COMMIT과 IMPLICIT_TRANSACTIONS를 OFF로 설정합니다. `CURSOR_CLOSE_ON_COMMIT` 및 `IMPLICIT_TRANSACTIONS`의 OFF 설정은 ODBC 데이터 원본에서, ODBC 연결 특성에서 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하기 전에 애플리케이션에서 설정되는 OLE DB 연결 속성에서 구성할 수 있습니다. DB-Library 애플리케이션 연결에 대한 `ANSI_DEFAULTS` 기본값은 OFF입니다.  
  
SET ANSI_DEFAULTS가 실행되면 QUOTED_IDENTIFIER 옵션은 구문 분석 시 설정되고 다음 옵션은 실행 시 설정됩니다.  
  
:::row:::
    :::column:::
        SET ANSI_NULLS
    :::column-end:::
    :::column:::
        SET ANSI_WARNINGS
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        SET ANSI_NULL_DFLT_ON
    :::column-end:::
    :::column:::
        SET CURSOR_CLOSE_ON_COMMIT
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        SET ANSI_PADDING
    :::column-end:::
    :::column:::
        SET IMPLICIT_TRANSACTIONS
    :::column-end:::
:::row-end:::

## <a name="permissions"></a>사용 권한  
**public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
다음 예에서는 ANSI_DEFAULTS를 ON으로 설정하고 `DBCC USEROPTIONS` 문을 사용하여 영향을 받는 설정을 표시합니다.  
  
```sql  
-- SET ANSI_DEFAULTS ON.  
SET ANSI_DEFAULTS ON;  
GO  

-- Display the current settings.  
DBCC USEROPTIONS;  
GO 

-- SET ANSI_DEFAULTS OFF.  
SET ANSI_DEFAULTS OFF;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [DBCC USEROPTIONS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)   
 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CURSOR_CLOSE_ON_COMMIT&#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)   
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
