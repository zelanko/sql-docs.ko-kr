---
description: 열의 기본값 지정
title: 열의 기본값 지정 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2020
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], defaults
- default values
ms.assetid: 64514aed-b846-407b-992e-cf813f9a1a91
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4ef2e6eebd15d2d88d9bed1290614d67b5596b87
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474604"
---
# <a name="specify-default-values-for-columns"></a>열의 기본값 지정

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 테이블 열에 입력될 기본값을 지정할 수 있습니다. 사용자 인터페이스의 개체 탐색기를 사용하거나 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 제출하여 기본값을 설정할 수 있습니다.

열에 기본값을 할당하지 않은 상태에서 사용자가 열을 비워 두면 다음과 같은 결과가 발생합니다.

- Null 값이 허용되도록 옵션을 설정한 경우 NULL이 열에 삽입됩니다.

- Null 값을 허용하는 옵션을 설정하지 않은 경우 열이 빈 채로 남겨지지만 사용자가 열의 값을 입력하지 않으면 행을 저장할 수 없습니다.

## <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항

시작하기 전에 다음 주의 사항에 유의하세요.

- **기본값** 필드에 값을 입력하여 괄호 없이 표시되는 바인딩된 기본값을 바꾸려는 경우 기본값을 바인딩 해제하고 새 기본값으로 대체하라는 메시지가 나타납니다.

- 텍스트 문자열을 입력하려면 값을 작은따옴표(')로 묶어야 합니다. 큰따옴표(")는 따옴표 붙은 식별자용으로 예약되어 있으므로 사용하지 않아야 합니다.

- 숫자 기본값을 입력하려면 따옴표를 사용하지 않고 숫자를 입력합니다.

- 개체/함수를 입력하려면 따옴표 없이 개체/함수의 이름을 입력합니다.

### <a name="security-permissions"></a><a name="Security"></a> 보안 권한

이 문서에 설명된 작업에는 테이블에 대한 ALTER 권한이 필요합니다.

## <a name="use-ssms-to-specify-a-default"></a><a name="SSMSProcedure"></a> SSMS를 사용하여 기본값 지정

개체 탐색기를 사용하여 테이블 열의 기본값을 지정할 수 있습니다.

### <a name="object-explorer"></a>개체 탐색기

1. **개체 탐색기** 에서 소수 자릿수를 변경할 열이 포함된 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인** 을 클릭합니다.

2. 기본값을 지정하려는 열을 선택합니다.

3. **열 속성** 탭에서 **기본값 또는 바인딩** 속성에 새 기본값을 입력합니다.

   > [!NOTE]
   > 숫자 기본값을 입력하려면 숫자를 입력합니다. 개체나 함수의 경우 해당 이름을 입력합니다. 영숫자 기본값의 경우 원하는 값을 작은따옴표로 묶어 입력합니다.

4. **파일** 메뉴에서 ‘테이블 이름’ **저장을 클릭합니다.** 

## <a name="use-transact-sql-to-specify-a-default"></a><a name="TsqlProcedure"></a> Transact-SQL을 사용하여 기본값 지정

SSMS를 사용하여 T-SQL을 제출하면 다양한 방법으로 열의 기본값을 지정할 수 있습니다.

### <a name="alter-table-t-sql"></a>ALTER TABLE(T-SQL)

1. **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.

2. 표준 도구 모음에서 **새 쿼리** 를 클릭합니다.

3. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.

   ```sql
   CREATE TABLE dbo.doc_exz (column_a INT, column_b INT); -- Allows nulls.
   GO
   INSERT INTO dbo.doc_exz (column_a) VALUES (7);
   GO
   ALTER TABLE dbo.doc_exz
     ADD CONSTRAINT DF_Doc_Exz_Column_B
     DEFAULT 50 FOR column_b;
   GO
   ```

<!--
The following two T-SQL code examples were offered by 'nycdotnet' (Steve) via public PR 1660, Feb 2019.
-->

### <a name="create-table-t-sql"></a>CREATE TABLE(T-SQL)

```sql
    CREATE TABLE dbo.doc_exz (
      column_a INT,
      column_b INT DEFAULT 50);
```

### <a name="named-constraint-t-sql"></a>명명된 CONSTRAINT(T-SQL)

```sql
    CREATE TABLE dbo.doc_exz (
      column_a INT,
      column_b INT CONSTRAINT DF_Doc_Exz_Column_B DEFAULT 50);
```

자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.
