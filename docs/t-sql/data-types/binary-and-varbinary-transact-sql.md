---
title: binary 및 varbinary(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 8/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: eb67f7bbfe21b1e213e5ef166b54f91ae4b3513c
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39454997"
---
# <a name="binary-and-varbinary-transact-sql"></a>binary 및 varbinary(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

고정 길이 또는 가변 길이의 이진 데이터 형식입니다.
  
## <a name="arguments"></a>인수  
**binary** [(*n*)] 길이가 *n*바이트인 고정 길이의 이진 데이터입니다. 여기서 *n*은 1부터 8,000까지의 값입니다. 저장소 크기는 *n*바이트입니다.
  
**varbinary** [(*n* | **max**)] 가변 길이 이진 데이터입니다. *n*은 1부터 8000 사이의 값이 될 수 있습니다. **max**는 최대 저장소 크기가 2^31-1바이트임을 나타냅니다. 저장소 크기는 입력된 실제 데이터 길이에 2바이트를 더한 값입니다. 입력된 데이터의 길이가 0바이트일 수 있습니다. **varbinary**의 ANSI SQL 동의어는 **binary varying**입니다.
  
## <a name="remarks"></a>Remarks  
데이터 정의나 변수 선언문에서 *n*을 지정하지 않으면 기본 길이 1이 사용됩니다. CAST 함수에 *n*을 지정하지 않으면 기본 길이 30이 사용됩니다.

| 데이터 형식 | 사용 시기... |
| --- | --- |
| **binary** | 열 데이터 항목의 크기가 일관적입니다.|
| **varbinary** | 열 데이터 항목의 크기가 상당히 다릅니다.|
| **varbinary(max)** | 열 데이터 항목이 8,000바이트를 초과합니다.|


## <a name="converting-binary-and-varbinary-data"></a>binary 및 varbinary 데이터 변환
데이터가 문자열 데이터 형식(**char**, **varchar**, **nchar**, **nvarchar**, **binary**, **varbinary**, **text**, **ntext**, 또는 **image**)에서 길이가 다른 **binary** 또는 **varbinary** 데이터 형식으로 변환될 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 오른쪽의 데이터를 패딩하거나 자릅니다. 다른 데이터 형식을 **binary** 또는 **varbinary**로 변환하면 데이터의 왼쪽이 패딩되거나 잘립니다. 패딩은 16진수 0을 사용하여 수행됩니다.
  
데이터를 **binary** 및 **varbinary** 데이터 형식으로 변환하는 것은 **binary** 데이터가 데이터를 이동하는 가장 쉬운 방법인 경우에 유용합니다. 두 변환이 같은 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 수행된 경우 형식의 값을 아주 큰 이진 값으로 변환한 다음 다시 이전 형식으로 변환하면 항상 같은 값을 갖게 됩니다. 값의 이진 표현은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전을 변경합니다.
  
**int**, **smallint** 및 **tinyint**를 **binary** 또는 **varbinary**로 변환할 수 있지만, **binary** 값을 다시 정수 값으로 변환하는 경우 잘림이 발생하면 이 값은 원래 정수 값과 달라집니다. 예를 들어 다음 SELECT 문은 정수 값 `123456`이 일반적으로 이진 `0x0001e240`으로 저장됨을 보여 줍니다.
  
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
  
최종 결과는 `57921`이 아니라 `123457`입니다.
  
> [!NOTE]  
>  모든 데이터 형식과 **binary** 데이터 형식 간의 변환은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전 사이에서 같다고 보장할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[데이터 형식 변환&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
