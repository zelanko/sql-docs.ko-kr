---
title: binary 및 varbinary(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- binary_TSQL
- varbinary_TSQL
- binary
- varbinary
dev_langs:
- TSQL
helpviewer_keywords:
- varbinary data type
- binary [SQL Server], about binary data type
ms.assetid: bcce65f9-10db-4b3e-bfaf-dfc06c6f820f
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f267da97eeb409be81bfcca71af602ebce1ffe1c
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86548746"
---
# <a name="binary-and-varbinary-transact-sql"></a>binary 및 varbinary(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

고정 길이 또는 가변 길이의 이진 데이터 형식입니다.
  
## <a name="arguments"></a>인수

**binary** [(_n_)] 길이가 _n_바이트인 고정 길이의 이진 데이터입니다. 여기서 _n_은 1부터 8,000까지의 값입니다. 스토리지 크기는 _n_ 바이트입니다.
  
**varbinary** [(_n_ | **max**)] 가변 길이 이진 데이터입니다. _n_은 1부터 8000 사이의 값이 될 수 있습니다. **max**는 최대 스토리지 크기가 2^31-1바이트임을 나타냅니다. 스토리지 크기는 입력된 실제 데이터 길이에 2바이트를 더한 값입니다. 입력된 데이터의 길이가 0바이트일 수 있습니다. **varbinary**의 ANSI SQL 동의어는 **binary varying**입니다.
  
## <a name="remarks"></a>설명  
데이터 정의나 변수 선언문에서 _n_을 지정하지 않은 경우 기본 길이는 1입니다. CAST 함수에 _n_을 지정하지 않은 경우 기본 길이는 30입니다.

| 데이터 형식 | 사용 시기... |
| --- | --- |
| **binary** | 열 데이터 항목의 크기가 일관적입니다.|
| **varbinary** | 열 데이터 항목의 크기가 상당히 다릅니다.|
| **varbinary(max)** | 열 데이터 항목이 8,000바이트를 초과합니다.|


## <a name="converting-binary-and-varbinary-data"></a>binary 및 varbinary 데이터 변환
문자열 데이터 형식에서 길이가 다른 **binary** 또는 **varbinary** 데이터 형식으로 데이터를 변환하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 오른쪽의 데이터를 패딩하거나 자릅니다. 문자열 데이터 형식은 다음과 같습니다.

* **char** 
* **varchar**
* **nchar**
* **nvarchar**
* **binary**
* **varbinary**
* **text**
* **ntext**
* **image**

다른 데이터 형식을 **binary** 또는 **varbinary**로 변환하면 데이터의 왼쪽이 패딩되거나 잘립니다. 패딩은 16진수 0을 사용하여 수행됩니다.
  
데이터를 **binary** 및 **varbinary** 데이터 형식으로 변환하는 것은 **binary** 데이터가 데이터를 이동하는 가장 쉬운 방법인 경우에 유용합니다. 특정 시점에 값 형식을 충분히 큰 크기의 이진 값으로 변환한 후 다시 이전 형식으로 변환할 수 있습니다. 두 변환이 같은 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 수행된 경우 이 변환에서는 항상 같은 값이 생성됩니다. 값의 이진 표현은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전을 변경합니다.
  
**int**, **smallint** 및 **tinyint**를 **binary** 또는 **varbinary**로 변환할 수 있습니다. **binary** 값을 다시 정수 값으로 변환하는 경우 잘림이 발생하면 이 값이 원래 정수 값과 달라집니다. 예를 들어 다음 SELECT 문은 정수 값 `123456`이 이진 `0x0001e240`으로 저장됨을 보여 줍니다.
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
그러나 다음 `SELECT` 문에서 **binary** 대상이 전체 값을 저장하기에 너무 작으면 동일한 숫자가 `0xe240`으로 저장되도록 선행 숫자가 자동으로 잘리는 것을 볼 수 있습니다.
  
```sql
SELECT CAST( 123456 AS BINARY(2) );  
```  
  
다음 일괄 처리는 자동 잘림이 오류를 일으키지 않고 산술 연산에 영향을 줄 수 있음을 보여 줍니다.
  
```sql
DECLARE @BinaryVariable2 BINARY(2);  
  
SET @BinaryVariable2 = 123456;  
SET @BinaryVariable2 = @BinaryVariable2 + 1;  
  
SELECT CAST( @BinaryVariable2 AS INT);  
GO  
```  
  
최종 결과는 `123457`이 아니라 `57921`입니다.
  
> [!NOTE]  
>  모든 데이터 형식과 **binary** 데이터 형식 간의 변환은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전 사이에서 같다고 보장할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[데이터 형식 변환&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
