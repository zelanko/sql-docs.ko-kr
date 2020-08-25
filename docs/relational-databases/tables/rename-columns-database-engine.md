---
description: 열 이름 바꾸기(데이터베이스 엔진)
title: 열 이름 바꾸기(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], names
- renaming columns
- column names [SQL Server]
ms.assetid: 7c71ec9f-0180-4398-b32a-4bfb7592e75d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 18ed629f6a9d02c0068a20fc1da3e8d5c4375dc2
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645805"
---
# <a name="rename-columns-database-engine"></a>열 이름 바꾸기(데이터베이스 엔진)


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 테이블 열의 이름을 바꿀 수 있습니다.

**항목 내용**

- **시작하기 전 주의 사항:**

   [제한 사항](#Restrictions)

   [보안](#Security)

- **다음을 사용하여 열 이름을 바꿉니다.**

   [SQL Server Management Studio](#SSMSProcedure)

   [Transact-SQL](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에

### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항

열 이름을 변경해도 해당 열에 대한 참조 이름은 자동으로 바뀌지 않습니다. 이름을 변경한 열을 참조하는 개체는 수동으로 수정해야 합니다. 예를 들어 테이블 열의 이름을 변경하고 이 열이 트리거에서 참조되는 경우 트리거를 수정하여 새로운 열 이름을 적용해야 합니다. [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 를 사용하여 이 개체에 종속된 개체를 나열한 다음 개체의 이름을 변경할 수 있습니다.

### <a name="security"></a><a name="Security"></a> 보안

#### <a name="permissions"></a><a name="Permissions"></a> 권한

개체에 대한 ALTER 사용 권한이 필요합니다.

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용

### <a name="to-rename-a-column-using-object-explorer"></a>개체 탐색기를 사용하여 열 이름을 바꾸려면

1. **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.
2. **개체 탐색기**에서 열 이름을 바꾸려는 테이블을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택합니다.
3. 새 열 이름을 입력합니다.

### <a name="to-rename-a-column-using-table-designer"></a>테이블 디자이너를 사용하여 열 이름을 바꾸려면

1. **개체 탐색기**에서 열 이름을 바꾸려는 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.
2. **열 이름**아래에서 변경하려는 이름을 선택하고 새 이름을 입력합니다.
3. **파일** 메뉴에서 ‘테이블 이름’ **저장을 클릭합니다.** __

> [!NOTE]
> **열 속성** 탭에서 열 이름을 변경할 수도 있습니다. 이름을 변경하려는 열을 선택하고 **이름**에 새 이름을 입력합니다.

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용

**열 이름을 바꾸려면**

### <a name="to-rename-a-column"></a>열 이름을 바꾸려면

다음 예제에서는 AdventureWorks 데이터베이스에서 `Sales.SalesTerritory` 테이블에 있는 `TerritoryID` 열의 이름을 `TerrID`로 바꿉니다.

```sql
EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';
```

자세한 내용은 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)을 참조하세요.
