---
title: "binary 및 varbinary (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 8/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4ad5bce3cacc0f892f7087df785da8cedcb4e932
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="binary-and-varbinary-transact-sql"></a>binary 및 varbinary(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이진 데이터 형식의 길이 또는 가변 길이 수정 했습니다.
  
## <a name="arguments"></a>인수  
**이진** [(  *n*  )]의 길이가 고정 길이 이진 데이터  *n*  바이트, 여기서  *n*  값 1부터 8,000 사이의 합니다. 저장소 크기는  *n*  바이트입니다.
  
**varbinary** [(  *n*   |  **max**)] 가변 길이 이진 데이터입니다. *n*1부터 8,000 사이의 값일 수 있습니다. **최대** 중임을 최대 저장소 크기가 2 ^31-1 바이트입니다. 저장소 크기는 입력된 실제 데이터 길이에 2바이트를 더한 값입니다. 입력된 데이터의 길이가 0바이트일 수 있습니다. 에 대 한 ANSI SQL 동의어 **varbinary** 은 **binary varying**합니다.
  
## <a name="remarks"></a>주의  
때  *n*  기본 길이 1 데이터 정의 나 변수 선언문에서 지정 하지 않으면 합니다. 때  *n*  기본 길이 30 CAST 함수를 지정 하지 않으면 합니다.

| 데이터 형식 | 사용 시기 |
| --- | --- |
| **binary** | 열 데이터 항목의 크기는 일치 합니다.|
| **varbinary** | 열 데이터 항목의 크기를 크게 달라 집니다.|
| **varbinary(max)** | 열 데이터 항목 8, 000 바이트를 초과합니다.|


## <a name="converting-binary-and-varbinary-data"></a>Binary 및 varbinary 데이터 변환
데이터가 문자열 데이터 형식에서 변환 됩니다 때 (**char**, **varchar**, **nchar**, **nvarchar**, **이진**, **varbinary**, **텍스트**, **ntext**, 또는 **이미지**)에 **이진** 또는 **varbinary** 데이터 형식의 길이가 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 채우거 나 오른쪽에 있는 데이터를 자릅니다. 다른 데이터 형식을 변환할 때 **이진** 또는 **varbinary**, 데이터 채워지거나 왼쪽에서 잘립니다. 패딩은 16진수 0을 사용하여 수행됩니다.
  
데이터를 변환는 **이진** 및 **varbinary** 데이터 형식이 유용 경우 **이진** 데이터는 데이터에 대 한 이동 하는 가장 쉬운 방법입니다. 값 변환 충분 한 크기의 큰 이진 값을 입력 한 다음에서 형식으로 다시 항상 결과 값과 동일한 값에서 두 변환이 같은 버전의에서 수행 되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 값의 이진 표현은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전을 변경합니다.
  
변환할 수 **int**, **smallint**, 및 **tinyint** 를 **이진** 또는 **varbinary**, 경우에 있습니다 변환 된 **이진** 잘림이 발생 한 경우 값이이 값을 정수 값으로 다시 원래 정수 값과에서 다 됩니다. 예를 들어 다음 SELECT 문은 정수 값 `123456`이 일반적으로 이진 `0x0001e240`으로 저장됨을 보여 줍니다.
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
그러나 다음 `SELECT` 문은 표시 되는 경우는 **이진** 대상이 전체 값을 보유할 너무 작아서, 동일한 수로 저장 되도록 선행 숫자가 자동으로 잘리는 `0xe240`:
  
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
>  입력 데이터 간의 변환 및 **이진** 데이터 형식은의 버전 간에 동일 하 게 보장 되지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[데이터 형식 변환 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
