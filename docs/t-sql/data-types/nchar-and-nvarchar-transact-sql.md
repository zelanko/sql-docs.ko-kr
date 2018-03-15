---
title: "nchar 및 nvarchar(Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/22/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4c3f2e9ad1d63992be8f4e4a4c65d821fae73389
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar 및 nvarchar(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

고정 길이(**nchar**) 또는 가변 길이(**nvarchar**) 유니코드 데이터이며 UNICODE UCS-2 문자 집합을 사용하는 문자 데이터 형식입니다.
  
## <a name="arguments"></a>인수  
**nchar** [ ( n ) ]  
고정 길이 유니코드 문자열 데이터. *n*은 문자열 길이를 정의하며 1에서 4,000 사이여야 합니다. 저장소 크기는 *n* 바이트의 두 배입니다. 데이터 정렬 코드 페이지에서 더블바이트 문자를 사용할 경우 저장소 크기는 계속 *n*바이트입니다. 문자열에 따라 *n*바이트의 저장소 크기가 *n*에 지정된 값보다 작을 수도 있습니다. **nchar**의 ISO 동의어는 **national char**와 **national character**입니다.
  
**nvarchar** [ ( n | **max** ) ]  
가변 길이 유니코드 문자열 데이터입니다. *n*은 문자열 길이를 정의하며 1에서 4,000 사이가 될 수 있습니다. **max**는 최대 저장소 크기가 2^31-1자(2 GB)임을 나타냅니다. 저장소 크기(바이트)는 입력된 데이터의 실제 길이의 두 배 + 2바이트입니다. **nvarchar**의 ISO 동의어는 **national char varying** 및 **national character varying**로 다양합니다.
  
## <a name="remarks"></a>Remarks  
데이터 정의나 변수 선언문에서 *n*을 지정하지 않으면 기본 길이 1이 사용됩니다. CAST 함수에 *n*을 지정하지 않으면 기본 길이 30이 사용됩니다.
  
열 데이터 항목들의 크기가 비슷할 경우 **nchar**를 사용합니다.
  
열 데이터 항목들의 크기가 다양할 경우 **nvarchar**를 사용합니다.
  
**sysname**은 시스템이 제공하는 사용자 정의 데이터 형식으로 Null을 허용하지 않는다는 점을 제외하면 기능상 **nvarchar(128)**와 동일합니다. **sysname**은 데이터베이스 개체 이름을 참조하는 데 사용됩니다.
  
**nchar** 또는 **nvarchar**를 사용하는 개체에는 COLLATE 절을 사용하여 특정 데이터 정렬을 할당하지 않는 한 데이터베이스의 기본 데이터 정렬이 할당됩니다.
  
SET ANSI_PADDING은 **nchar** 및 **nvarchar**에 대해 항상 ON입니다. SET ANSI_PADDING OFF는 **nchar** 또는 **nvarchar** 데이터 형식에 적용되지 않습니다.
  
유니코드 문자열 상수에 문자 N을 접두사로 붙입니다. N 접두사가 없으면 문자열은 데이터베이스의 기본 코드 페이지로 변환됩니다. 이 기본 코드 페이지는 일부 문자를 인식하지 않을 수 있습니다.
 
> [!NOTE]  
>  문자열 상수 앞에 문자 N을 붙일 때 변환할 상수가 유니코드 문자열 데이터 유형(4,000)의 최대 길이를 초과하지 않는 경우 암시적 변환의 결과 유니 코드 문자열이 됩니다. 그렇지 않은 경우 암시적 변환으로 유니코드 큰 값(최대)이 됩니다.
  
> [!WARNING]  
>  Null이 아닌 각 **varchar(max)** 또는 **nvarchar(max)** 열은 24바이트의 추가 고정 할당을 필요로 하며 이는 정렬 작업 동안에 적용되는 8,060바이트 행 제한에 반해서 집계됩니다. 이로 인해 null이 아닌 **varchar(max)**의 수 또는 테이블에서 생성할 수 있는 **nvarchar(max)** 열의 수에 암묵적인 제한이 생깁니다. 테이블 생성 시 또는 데이터 삽입 시점에 특별한 오류(최대 행의 크기가 최대로 허용된 8060바이트를 초과한다는 일반적인 경고 외의 메시지)가 표시되지 않습니다. 이렇게 크기가 큰 행은 클러스터형 인덱스 키 업데이트 같은 일부 정상 작업이나 전체 열 집합 정렬에서 오류(오류 512 등)를 발생시킬 수 있고 사용자는 이러한 오류를 작업을 수행하기 전에는 예측할 수 없습니다.  
  
## <a name="converting-character-data"></a>문자 데이터 변환  
문자 데이터 변환에 대한 자세한 내용은 [char 및 varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)를 참조하세요.
  
## <a name="examples"></a>예  
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyNCharColumn nchar(15)  
,MyNVarCharColumn nvarchar(20)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (N'Test data', N'More test data');  
GO  
SELECT MyNCharColumn, MyNVarCharColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyNCharColumn   MyNVarCharColumn  
--------------- --------------------  
Test data       More test data  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)
  
  
