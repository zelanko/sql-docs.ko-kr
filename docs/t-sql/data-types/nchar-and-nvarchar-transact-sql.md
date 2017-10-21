---
title: "nchar 및 nvarchar (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc7de3b64519f3d0fd1f2e9557ccf7196e3f07a8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar 및 nvarchar(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

문자 데이터 형식 중 하나가 고정 길이,입니다 **nchar**, 또는 가변 길이 **nvarchar**, 유니코드 데이터와 사용 하 여 UNICODE ucs-2 문자 집합입니다.
  
## <a name="arguments"></a>인수  
**nchar** [(n)]  
고정 길이 유니코드 문자열 데이터. *n*문자열 길이 정의 하며 1과 4,000 사이의 값 이어야 합니다. 저장소 크기는 두 번  *n*  바이트입니다. 데이터 정렬 코드 페이지에서 더블 바이트 문자를 사용할 경우 저장소 크기는 여전히  *n*  바이트입니다. 문자열의 저장소 크기에 따라  *n*  바이트에 대 한 지정 된 값 보다 작을 수 있으며  *n* 합니다. ISO 동의어 **nchar** 는 **national char** 및 **국가별 문자**...
  
**nvarchar** [(n | **최대** )]  
가변 길이 유니코드 문자열 데이터입니다. *n*문자열 길이 정의 하며 1에서 4,000 사이가 될 수 있습니다. **최대** 중임을 최대 저장소 크기가 2 ^31-1 바이트 (2GB)입니다. 저장소 크기(바이트)는 입력된 데이터의 실제 길이의 두 배 + 2바이트입니다. ISO 동의어 **nvarchar** 는 **다양 한 national char** 및 **국가별 문자 다양 한**합니다.
  
## <a name="remarks"></a>주의  
때  *n*  기본 길이 1 데이터 정의 나 변수 선언문에서 지정 하지 않으면 합니다. 때  *n*  기본 길이 30 CAST 함수를 지정 하지 않으면 합니다.
  
사용 하 여 **nchar** 열 데이터 항목의 크기가 비슷할 하려는 것입니다.
  
사용 하 여 **nvarchar** 열 데이터 항목의 크기가 다를 하려는 것입니다.
  
**sysname** 기능적으로 시스템 제공 하는 사용자 정의 데이터 형식이 **nvarchar (128)**제외 하 고 null을 허용 하지 않습니다. **sysname** 데이터베이스 개체 이름을 참조 하는 데 사용 됩니다.
  
사용 하는 개체 **nchar** 또는 **nvarchar** COLLATE 절을 사용 하 여 특정 데이터 정렬을 할당 하지 않는 한 데이터베이스의 기본 데이터 정렬이 할당 됩니다.
  
SET ANSI_PADDING은 항상 ON으로 **nchar** 및 **nvarchar**합니다. SET ANSI_PADDING OFF에 적용 되지 않습니다는 **nchar** 또는 **nvarchar** 데이터 형식입니다.
  
붙이는와 유니코드 문자열 상수의 접두사로 접두사 N이 없으면 문자열이 데이터베이스의 기본 코드 페이지로 변환 됩니다. 이 기본 코드 페이지는 일부 문자를 인식하지 않을 수 있습니다.
 
> [!NOTE]  
>  문자열 상수와 문자 N 접두사를 추가 변환할 상수는 유니코드 문자열 데이터 형식 (4000)에 대 한 최대 길이 초과 하지 않는 경우 유니코드 문자열에 암시적 변환이 발생 합니다. 그렇지 않은 경우 암시적으로 변환 된 유니코드 큰 값 (최대)에서 발생 합니다.
  
> [!WARNING]  
>  Null이 아닌 각 **varchar (max)** 또는 **nvarchar (max)** 열 정렬 작업 동안 8, 060 바이트 행 제한에 따라 계산 하는 추가 고정된 할당의 24 바이트 필요 합니다. 이 null이 아닌 수에 암묵적인 제한이 생깁니다 **varchar (max)** 또는 **nvarchar (max)** 테이블에서 만들 수 있는 열입니다. 테이블 생성 시 또는 데이터 삽입 시점에 특별한 오류(최대 행의 크기가 최대로 허용된 8060바이트를 초과한다는 일반적인 경고 외의 메시지)가 표시되지 않습니다. 이렇게 크기가 큰 행은 클러스터형 인덱스 키 업데이트 같은 일부 정상 작업이나 전체 열 집합 정렬에서 오류(오류 512 등)를 발생시킬 수 있고 사용자는 이러한 오류를 작업을 수행하기 전에는 예측할 수 없습니다.  
  
## <a name="converting-character-data"></a>문자 데이터 변환  
문자 데이터를 변환 하는 방법에 대 한 정보를 참조 하십시오. [char 및 varchar&#40; Transact SQL &#41; ](../../t-sql/data-types/char-and-varchar-transact-sql.md).
  
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
  
## <a name="see-also"></a>참고 항목
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40; Transact SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[마찬가지로 &#40; Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ansi_padding&#40; Transact SQL &#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)
  
  

