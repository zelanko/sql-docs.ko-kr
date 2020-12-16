---
description: SQL Server 데이터 정렬 이름(Transact-SQL)
title: SQL Server Collation Name(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 092edef1c9e3c03b2d9c8b96569c131048a064d1
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489481"
---
# <a name="sql-server-collation-name-transact-sql"></a>SQL Server 데이터 정렬 이름(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬의 데이터 정렬 이름을 지정하는 단일 문자열입니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 Windows 데이터 정렬을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 Windows 데이터 정렬을 지원하기 전에 개발된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬이라는 제한된 수(<80)의 데이터 정렬도 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬은 이전 버전과의 호환성을 위해 계속 지원되지만 새로운 개발 작업에 사용해서는 안 됩니다. Windows 데이터 정렬에 대한 자세한 내용은 [Windows 데이터 정렬 이름](../../t-sql/statements/windows-collation-name-transact-sql.md)을 참조하세요.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```syntaxsql
<SQL_collation_name> :: =
SQL_SortRules[_Pref]_CPCodepage_<ComparisonStyle>

<ComparisonStyle> ::=
_CaseSensitivity_AccentSensitivity | _BIN
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수

*SortRules* 사전 정렬을 지정했을 때 정렬 규칙이 적용되는 알파벳 또는 언어를 나타내는 문자열입니다. 예를 들면 Latin1_General 또는 Polish 등이 있습니다.

**Pref** 대문자 우선을 지정합니다. 비교에서 대소문자를 구분하더라도 다른 차이가 없는 경우 대문자가 소문자보다 먼저 정렬됩니다.

*Codepage* 데이터 정렬에 사용되는 코드 페이지를 표시하는 1~4자리 숫자를 지정합니다. **CP1** 은 코드 페이지 1252를 지정하며 다른 모든 코드 페이지에 대해서는 완전한 코드 페이지 번호를 지정합니다. 예를 들어 **CP1251** 은 코드 페이지 1251을 지정하며 **CP850** 은 코드 페이지 850을 지정합니다.

*CaseSensitivity*
**CI** 는 대/소문자를 구분하지 않도록 지정하고 **CS** 는 대/소문자를 구분하도록 지정합니다.

*AccentSensitivity*
**AI** 는 악센트를 구분하지 않도록 지정하고 **AS** 는 악센트를 구분하도록 지정합니다.

**BIN** 사용할 이진 정렬 순서를 지정합니다.

## <a name="remarks"></a>설명

서버에서 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬을 나열하려면 다음 쿼리를 실행합니다.

```sql
SELECT * FROM sys.fn_helpcollations()
WHERE name LIKE 'SQL%';
```

> [!NOTE]
> 정렬 순서 ID 80의 경우 코드 페이지 1250과 이진 순서를 가진 Window 데이터 정렬을 사용하세요. 예를 들어, Albanian_BIN, Croatian_BIN, Czech_BIN, Romanian_BIN, Slovak_BIN, Slovenian_BIN.

## <a name="see-also"></a>참고 항목

- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [상수](../../t-sql/data-types/constants-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [선언 @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
- [table](../../t-sql/data-types/table-transact-sql.md)
- [sys.fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
