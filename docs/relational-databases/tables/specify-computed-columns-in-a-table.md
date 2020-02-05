---
title: 테이블에서 계산 열 지정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- computed columns, define
ms.assetid: 731a4576-09c1-47f0-a8f6-edd0b55679f4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 47d4cb0991bde851fbc6c6f3273a673dfdecf919
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68082561"
---
# <a name="specify-computed-columns-in-a-table"></a>테이블에서 계산 열 지정

[!INCLUDE[tsql-appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

계산 열은 해당 열에 PERSISTED 표시가 없는 한 테이블에 물리적으로 저장되지 않는 가상의 열입니다. 계산 열 식에서는 이 식이 속한 열의 값을 계산하기 위해 다른 열의 데이터를 사용할 수 있습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 계산 열의 식을 지정할 수 있습니다.

**항목 내용**

- **시작하기 전 주의 사항:**

   [제한 사항](#Limitations)

   [보안](#Security)

- **계산 열을 지정하려면**

   [SQL Server Management Studio](#SSMSProcedure)

   [Transact-SQL](#TsqlProcedure)

## <a name="BeforeYouBegin"></a> 시작하기 전에

### <a name="Limitations"></a> 제한 사항

- 계산 열은 DEFAULT 또는 FOREIGN KEY 제약 조건 정의로 사용하거나 NOT NULL 제약 조건 정의와 함께 사용할 수 없습니다. 그러나 계산 열 값이 명확한 식에 의해 정의되고 결과의 데이터 형식이 인덱스 열에 허용되는 경우에는 계산 열을 인덱스의 키 열이나 PRIMARY KEY 또는 UNIQUE 제약 조건의 일부로 사용할 수 있습니다. 예를 들어 테이블에 a와 b라는 정수 열이 있을 때 계산 열 a + b에는 인덱스를 작성할 수 있지만 계산 열 a+DATEPART(dd, GETDATE())는 다음 호출 시 값이 바뀌므로 인덱스를 작성할 수 없습니다.
- 계산 열은 INSERT 또는 UPDATE 문의 대상이 될 수 없습니다.

### <a name="Security"></a> 보안

#### <a name="Permissions"></a> 권한

테이블에 대한 ALTER 사용 권한이 필요합니다.

## <a name="SSMSProcedure"></a> SQL Server Management Studio 사용

### <a name="NewColumn"></a> 새 계산 열을 추가하려면

1. **개체 탐색기**에서 새 계산 열을 추가할 테이블을 확장합니다. **열** 을 마우스 오른쪽 단추로 클릭하고 **새 열**을 선택합니다.
2. 열 이름을 입력하고 기본 데이터 형식(**nchar**(10))을 적용합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 수식에 지정된 식에 데이터 형식 우선 순위 규칙을 적용하여 계산 열의 데이터 형식을 결정합니다. 예를 들어 수식에서 **money** 형식 열과 **int**형식 열을 참조하는 경우 데이터 형식의 우선 순위가 더 높으므로 계산 열은 **money** 형식입니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.
3. **열 속성** 탭에서 **계산 열 사양** 속성을 확장합니다.
4. **(수식)** 자식 속성에서 오른쪽에 있는 표 형태 셀에 현재 열의 식을 입력합니다. 예를 들어 `SalesTotal` 열에 입력한 수식이 `SubTotal+TaxAmt+Freight`일 경우 이 수식은 테이블의 각 행에 대해 이 열에 값을 추가합니다.

   > [!IMPORTANT]
   > 수식으로 데이터 형식이 다른 두 식을 결합할 경우 데이터 형식 우선 순위 규칙에 따라 우선 순위가 낮은 데이터 형식이 우선 순위가 높은 데이터 형식으로 변환됩니다. 이 암시적 변환이 지원되지 않으면 "`Error validating the formula for column column_name.`" 오류가 반환됩니다. CAST 또는 CONVERT 함수를 사용하여 데이터 형식 충돌을 해결합니다. 예를 들어 **nvarchar** 형식 열을 **int**형식 열과 결합할 경우 **수식에 표시된 대로 정수 형식을** nvarchar `('Prod'+CONVERT(nvarchar(23),ProductID))`로 변환해야 합니다. 자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.

5. **지속형** 자식 속성 드롭다운에서 **예** 또는 **아니요** 를 선택하여 데이터를 지속할지 여부를 지정합니다.

6. **파일** 메뉴에서 ‘테이블 이름’ **저장**을 클릭합니다. 

#### <a name="to-add-a-computed-column-definition-to-an-existing-column"></a>기존 열에 계산 열 정의를 추가하려면

1. **개체 탐색기**에서 변경할 열이 포함된 테이블을 마우스 오른쪽 단추로 클릭하고 **열** 폴더를 확장합니다.
2. 계산 열 수식을 지정할 열을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다. **확인**을 클릭합니다.
3. 새 열을 추가하고 이전 절차에 따라 새 계산 열을 추가하여 계산 열 수식을 지정합니다.

## <a name="TsqlProcedure"></a> Transact-SQL 사용

### <a name="to-add-a-computed-column-when-creating-a-table"></a>테이블을 만들 때 계산 열을 추가하려면

다음 예제에서는 `QtyAvailable` 열의 값을 `UnitPrice` 열의 값으로 곱하는 계산 열을 포함하는 테이블을 만듭니다.

```sql
CREATE TABLE dbo.Products
   (
      ProductID int IDENTITY (1,1) NOT NULL
      , QtyAvailable smallint
      , UnitPrice money
      , InventoryValue AS QtyAvailable * UnitPrice
    )
;
-- Insert values into the table.
INSERT INTO dbo.Products (QtyAvailable, UnitPrice)
   VALUES (25, 2.00), (10, 1.5)
;
-- Display the rows in the table.
SELECT ProductID, QtyAvailable, UnitPrice, InventoryValue
FROM dbo.Products
;
```

### <a name="to-add-a-new-computed-column-to-an-existing-table"></a>기존 테이블에 새 계산 열을 추가하려면

다음 예에서는 이전 예에서 만든 테이블에 새 열을 추가합니다.

```sql
ALTER TABLE dbo.Products ADD RetailValue AS (QtyAvailable * UnitPrice * 1.5)
;
```

필요에 따라 계산 값을 물리적으로 테이블에 저장하는 PERSISTED 인수를 추가합니다.

```sql
ALTER TABLE dbo.Products ADD RetailValue AS (QtyAvailable * UnitPrice * 1.5) PERSISTED
;
```

### <a name="to-change-an-existing-column-to-a-computed-column"></a>기존 열을 계산 열로 변경하려면

다음 예에서는 이전 예에서 추가한 열을 수정합니다.

```sql
ALTER TABLE dbo.Products DROP COLUMN RetailValue
;
GO
ALTER TABLE dbo.Products ADD RetailValue AS (QtyAvailable * UnitPrice * 1.5)
;
```

자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.
