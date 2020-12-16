---
description: 테이블에서 열 삭제
title: 테이블에서 열 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 04/11/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], deleting
- removing columns
- deleting columns
- dropping columns
ms.assetid: 0d8f6e4f-bc71-4fa3-8615-74249c8e072d
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4cd04595c9e866aae6200613057c0b5cf84a1a2f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462624"
---
# <a name="delete-columns-from-a-table"></a>테이블에서 열 삭제

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 테이블 열을 삭제하는 방법에 대해 설명합니다.

> [!CAUTION]
> 테이블에서 열을 삭제하면 여기에 포함된 모든 데이터가 삭제됩니다.

 **항목 내용**

- **시작하기 전 주의 사항:**

   [제한 사항](#Restrictions)

   [보안](#Security)

- **테이블에서 열을 삭제하려면**

   [SQL Server Management Studio](#SSMSProcedure)

   [Transact-SQL](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에

### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항

CHECK 제약 조건이 있는 열은 삭제할 수 없습니다. 먼저 제약 조건을 삭제해야 합니다.

테이블 디자이너를 사용할 때를 제외하고는 PRIMARY KEY 또는 FOREIGN KEY 제약 조건이나 기타 종속성이 있는 열을 삭제할 수 없습니다. 개체 탐색기 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용할 때는 먼저 열에서 모든 종속성을 제거해야 합니다.

### <a name="security"></a><a name="Security"></a> 보안

#### <a name="permissions"></a><a name="Permissions"></a> 권한

테이블에 대한 ALTER 사용 권한이 필요합니다.

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용

### <a name="to-delete-columns-by-using-object-explorer"></a>개체 탐색기를 사용하여 열을 삭제하려면

1. **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.
2. **개체 탐색기** 에서 열을 삭제할 테이블을 찾고 확장하여 열 이름을 표시합니다.
3. 삭제할 열을 마우스 오른쪽 단추로 클릭하고 **삭제** 를 선택합니다.
4. **개체 삭제** 대화 상자에서 **확인** 을 클릭합니다.

열에 제약 조건 또는 기타 종속성이 포함된 경우 **개체 삭제** 대화 상자에 오류 메시지가 표시됩니다. 참조된 제약 조건을 삭제하여 오류를 해결합니다.

### <a name="to-delete-columns-by-using-table-designer"></a>테이블 디자이너를 사용하여 열을 삭제하려면

1. **개체 탐색기** 에서 열을 삭제하려는 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인** 을 선택합니다.
2. 삭제하려는 열을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **열 삭제** 를 선택합니다.
3. 관계에 참여하는 열(FOREIGN KEY 또는 PRIMARY KEY)인 경우에는 선택한 열과 해당 관계의 삭제를 확인하는 메시지가 표시됩니다. **예** 를 선택합니다.

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용

### <a name="to-delete-columns"></a>열을 삭제하려면

다음 예제에서는 열을 삭제하는 방법을 보여 줍니다.

```sql
ALTER TABLE dbo.doc_exb DROP COLUMN column_b;
```

열에 제약 조건 또는 기타 종속성이 포함된 경우 오류 메시지가 표시됩니다. 참조된 제약 조건을 삭제하여 오류를 해결합니다.

추가 예제를 보려면 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.

## <a name="FollowUp"></a>
