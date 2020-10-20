---
description: nchar 및 nvarchar(Transact-SQL)
title: nchar 및 nvarchar(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6e4083a2e06ced4275af0938e222143fa255ff48
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037533"
---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar 및 nvarchar(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

고정 크기(**nchar**) 또는 가변 크기(**nvarchar**)인 문자 데이터 형식입니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [SC(보조 문자)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) 사용 데이터 정렬을 사용할 때 이러한 데이터 형식은 전체 범위의 [유니코드](../../relational-databases/collations/collation-and-unicode-support.md#Unicode_Defn) 문자 데이터를 저장하고 [UTF-16](https://www.wikipedia.org/wiki/UTF-16) 문자 인코딩을 사용합니다. SC가 아닌 데이터 정렬이 지정된 경우 이러한 데이터 형식은 [UCS-2](https://www.wikipedia.org/wiki/Universal_Coded_Character_Set#Encoding_forms) 문자 인코딩에서 지원하는 문자 데이터의 하위 집합만 저장합니다.

## <a name="arguments"></a>인수
**nchar** [ ( n ) ]  
고정 크기 문자열 데이터입니다. *n*은 바이트 쌍으로 문자열 크기를 정의하며 1에서 4,000 사이의 값이어야 합니다. 스토리지 크기는 *n*바이트의 두 배입니다. [UCS-2](https://www.wikipedia.org/wiki/UTF-16#U+0000_to_U+D7FF_and_U+E000_to_U+FFFF) 인코딩의 경우 스토리지 크기는 *n*바이트의 두 배이고 저장할 수 있는 문자 수도 *n*입니다. UTF-16 인코딩의 경우 스토리지 크기는 여전히 *n*바이트의 두 배이지만, 보조 문자가 2바이트 쌍([서로게이트 쌍](https://www.wikipedia.org/wiki/UTF-16#U+010000_to_U+10FFFF)이라고도 함)을 사용하기 때문에 저장할 수 있는 문자 수는 *n*보다 작을 수 있습니다. **nchar**의 ISO 동의어는 **national char**와 **national character**입니다.
  
**nvarchar** [ ( n | **max** ) ]  
가변 크기 문자열 데이터입니다. *n*은 바이트 쌍으로 문자열 길이를 정의하며 1에서 4,000 사이의 값일 수 있습니다. **max**는 최대 스토리지 크기가 2^30-1자(2GB)임을 나타냅니다. 스토리지 크기는 *n*바이트 + 2바이트의 두 배입니다. [UCS-2](https://www.wikipedia.org/wiki/UTF-16#U+0000_to_U+D7FF_and_U+E000_to_U+FFFF) 인코딩의 경우 스토리지 크기는 *n*바이트 + 2바이트의 두 배이고 저장할 수 있는 문자 수도 *n*입니다. UTF-16 인코딩의 경우 스토리지 크기는 여전히 *n*바이트 +2바이트의 두 배이지만, 보조 문자가 2바이트 쌍([서로게이트 쌍](https://www.wikipedia.org/wiki/UTF-16#U+010000_to_U+10FFFF)이라고도 함)을 사용하기 때문에 저장할 수 있는 문자 수는 *n*보다 작을 수 있습니다. **nvarchar**의 ISO 동의어는 **national char varying** 및 **national character varying**로 다양합니다.
  
## <a name="remarks"></a>설명  
[NCHAR(*n*) 및 NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)에서 *n*이 문자 수를 정의한다고 잘못 생각하는 경우가 많습니다. 그러나 [NCHAR(*n*) 및 NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)에서 *n*은 **바이트 쌍**의 문자열 길이(0~4,000)를 정의합니다. *n*은 저장할 수 있는 문자 수를 정의하지 않습니다. [CHAR(*n*) 및 VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md) 정의와 비슷합니다.   
이러한 오해는 유니코드 범위 0~65,535에 정의된 문자를 사용하는 경우 각 바이트 쌍당 하나의 문자를 저장할 수 있기 때문에 발생합니다. 그러나 더 높은 유니코드 범위(65,536~1,114,111)에서는 한 문자가 두 개의 바이트 쌍을 사용할 수 있습니다. 예를 들어 NCHAR(10)로 정의된 열에서 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 하나의 바이트 쌍을 사용하는 문자(유니코드 범위 0~65,535) 10자를 저장할 수 있지만, 두 개의 바이트 쌍을 사용하는 경우(유니코드 범위 65,536~1,114,111) 10자 미만을 저장할 수 있습니다. 유니코드 스토리지 및 문자 범위에 대한 자세한 내용은 [UTF-8과 UTF-16 간의 스토리지 차이점](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences)을 참조하세요.     

데이터 정의나 변수 선언문에서 *n*을 지정하지 않으면 기본 길이 1이 사용됩니다. CAST 함수에 *n*을 지정하지 않으면 기본 길이 30이 사용됩니다.

**nchar** 또는 **nvarchar**를 사용하는 경우 다음을 수행하는 것이 좋습니다.
- 열 데이터 항목의 크기가 일관된 경우 **nchar**를 사용합니다.  
- 열 데이터 항목의 크기가 비교적 큰 차이를 보일 경우 **nvarchar**를 사용합니다.  
- 열 데이터 항목들의 크기가 비교적 큰 차이를 보이고 문자열 길이가 4,000바이트 쌍을 초과할 수 있는 경우 **nvarchar(max)** 를 사용합니다.  
  
**sysname**은 시스템이 제공하는 사용자 정의 데이터 형식으로 Null을 허용하지 않는다는 점을 제외하면 기능상 **nvarchar(128)** 와 동일합니다. **sysname**은 데이터베이스 개체 이름을 참조하는 데 사용됩니다.
  
**nchar** 또는 **nvarchar**를 사용하는 개체에는 COLLATE 절을 사용하여 특정 데이터 정렬을 할당하지 않는 한 데이터베이스의 기본 데이터 정렬이 할당됩니다.
  
SET ANSI_PADDING은 **nchar** 및 **nvarchar**에 대해 항상 ON입니다. SET ANSI_PADDING OFF는 **nchar** 또는 **nvarchar** 데이터 형식에 적용되지 않습니다.
  
유니코드 문자 문자열 상수 앞에 N 문자를 추가하여 SC 데이터 정렬 사용 여부에 따라 UCS-2 또는 UTF-16 입력을 알립니다. N 접두사가 없으면 문자열이 특정 문자를 인식할 수 없는 데이터베이스의 기본 코드 페이지로 변환됩니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 UTF-8 사용 데이터 정렬이 사용될 때 기본 코드 페이지는 유니코드 UTF-8 문자 집합을 저장할 수 있습니다. 
 
> [!NOTE]  
> 문자열 상수 앞에 문자 N을 붙일 때 변환할 상수가 nvarchar 문자열 데이터 형식(4,000)의 최대 길이를 초과하지 않는 경우 암시적 변환의 결과 UCS-2 또는 UTF-16 문자열이 됩니다. 그렇지 않은 경우 암시적 변환으로 nvarchar 큰 값(최대)이 됩니다.
  
> [!WARNING]  
> Null이 아닌 각 **varchar(max)** 또는 **nvarchar(max)** 열은 24바이트의 추가 고정 할당이 필요하며 정렬 작업 시 여기에 8,060바이트의 행 제한이 적용됩니다. 이러한 추가 바이트로 인해 테이블에서 null이 아닌 **varchar(max)** 또는 **nvarchar(max)** 열의 수에 묵시적 제한이 적용됩니다. 테이블 생성 시 또는 데이터 삽입 시점에 특별한 오류(최대 행의 크기가 최대로 허용된 8,060바이트를 초과한다는 일반적인 경고 외의 메시지)가 표시되지 않습니다. 이렇게 큰 행 크기로 인해 사용자가 일부 정상 작업 중 예기치 않은 오류가 발생할 수 있습니다(예: 오류 512).  작업의 두 가지 예제는 클러스터형 인덱스 키 업데이트 또는 전체 열 집합의 종류입니다.
  
## <a name="converting-character-data"></a>문자 데이터 변환  
문자 데이터 변환에 대한 자세한 내용은 [char 및 varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)를 참조하세요.
  
## <a name="see-also"></a>참고 항목
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE&#40;Transact-SQL&#41;](../statements/collations.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[LIKE&#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)    
[데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)     
[싱글바이트 및 멀티바이트 문자 집합](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)  
