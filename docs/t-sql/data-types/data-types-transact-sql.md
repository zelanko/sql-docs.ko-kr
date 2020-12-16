---
title: Data types(Transact-SQL) | Microsoft Docs
description: 이 문서에는 SQL Server에서 사용할 수 있는 다양한 데이터 형식이 요약되어 있습니다.
ms.date: 09/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system data types [SQL Server]
- data types [SQL Server]
- data types [SQL Server], about data types
ms.assetid: a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5039e7ea667c80b051413b93fbb34d2f4adc1038
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484335"
---
# <a name="data-types-transact-sql"></a>Data types(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 각 열, 지역 변수, 식 및 매개 변수는 관련된 데이터 형식을 가집니다. 데이터 형식은 개체가 보유할 수 있는 정수 데이터, 문자 데이터, 통화 데이터, 날짜 및 시간 데이터, 이진 문자열 등의 데이터 형식을 지정하는 특성입니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 있는 모든 데이터 형식을 정의하는 일련의 시스템 데이터 형식을 제공합니다. 또한 사용자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에서 사용자 고유의 데이터 형식을 정의할 수 있습니다. 별칭 데이터 형식은 시스템이 제공하는 데이터 형식을 기반으로 합니다. 별칭 데이터 형식에 대한 자세한 내용은 [CREATE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)을 참조하십시오. 사용자 정의 형식의 특징은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에서 지원하는 프로그래밍 언어 중 하나로 만든 클래스의 메서드 및 연산자에서 가져옵니다.
  
데이터 형식, 데이터 정렬, 전체 자릿수, 소수 자릿수 또는 길이가 다른 두 식이 연산자에 의해 결합된 경우 그 특징은 다음 규칙에 따라 결정됩니다.
-   결합 결과의 데이터 형식은 입력 식의 데이터 형식에 데이터 형식 우선 순위 규칙을 적용하여 결정됩니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
-   결과 데이터 형식이 **char**, **varchar**, **text**, **nchar**, **nvarchar** 또는 **ntext** 인 경우 결과의 데이터 정렬은 데이터 정렬 우선 순위 규칙에 따라 결정됩니다. 자세한 내용은 [데이터 정렬 선행 규칙&#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)을 참조하세요.  
-   결과의 전체 자릿수, 소수 자릿수 및 길이는 입력 식의 전체 자릿수, 소수 자릿수, 길이에 따라 달라집니다. 자세한 내용은 [전체 자릿수, 소수 자릿수 및 길이&#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)를 참조하세요.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 ISO 호환성을 위해 데이터 형식 동의어를 제공합니다. 자세한 내용은 [데이터 형식 동의어&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md)를 참조하세요.
  
## <a name="data-type-categories"></a>데이터 형식 범주
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터 형식은 다음 범주로 구성됩니다.
  
:::row:::
    :::column:::
        정확한 수치
    :::column-end:::
    :::column:::
        유니코드 문자열
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        근사치
    :::column-end:::
    :::column:::
        이진 문자열
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        날짜 및 시간
    :::column-end:::
    :::column:::
        기타 데이터 형식
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        문자열
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 일부 데이터 형식은 스토리지 특징에 따라 다음 그룹에 속하도록 지정됩니다.
-   Large value 데이터 형식: **varchar(max)** , **nvarchar(max)**  
-   Large object 데이터 형식: **text**, **ntext**, **image**, **varbinary(max)** , **xml**  
  
    > [!NOTE]  
    >  sp_help는 큰 값 및 **xml** 데이터 형식의 길이로 -1을 반환합니다.  
  
### <a name="exact-numerics"></a>정확한 수치
  
:::row:::
    :::column:::
        [bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)
    :::column-end:::
    :::column:::
        [numeric](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [bit](../../t-sql/data-types/bit-transact-sql.md)
    :::column-end:::
    :::column:::
        [smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [decimal](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)
    :::column-end:::
    :::column:::
        [smallmoney](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)
    :::column-end:::
    :::column:::
        [tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

### <a name="approximate-numerics"></a>근사치
  
:::row:::
    :::column:::
        [float](../../t-sql/data-types/float-and-real-transact-sql.md)
    :::column-end:::
    :::column:::
        [real](../../t-sql/data-types/float-and-real-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

### <a name="date-and-time"></a>날짜 및 시간
  
:::row:::
    :::column:::
        [date](../../t-sql/data-types/date-transact-sql.md)
    :::column-end:::
    :::column:::
        [datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [datetime2](../../t-sql/data-types/datetime2-transact-sql.md)
    :::column-end:::
    :::column:::
        [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [datetime](../../t-sql/data-types/datetime-transact-sql.md)
    :::column-end:::
    :::column:::
        [time](../../t-sql/data-types/time-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
  
### <a name="character-strings"></a>문자열
  
:::row:::
    :::column:::
        [char](../../t-sql/data-types/char-and-varchar-transact-sql.md)
    :::column-end:::
    :::column:::
        [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [text](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
 
### <a name="unicode-character-strings"></a>유니코드 문자열
  
:::row:::
    :::column:::
        [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)
    :::column-end:::
    :::column:::
        [nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
  

### <a name="binary-strings"></a>이진 문자열
  
:::row:::
    :::column:::
        [binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)
    :::column-end:::
    :::column:::
        [varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [image](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

### <a name="other-data-types"></a>기타 데이터 형식

:::row:::
    :::column:::
        [cursor](../../t-sql/data-types/cursor-transact-sql.md)
    :::column-end:::
    :::column:::
        [rowversion](../../t-sql/data-types/rowversion-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [hierarchyid](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
    :::column-end:::
    :::column:::
        [uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)
    :::column-end:::
    :::column:::
        [xml](../../t-sql/xml/xml-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [공간 geometry 형식](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md) 
    :::column-end:::
    :::column:::
        [공간 지리 형식](../../t-sql/spatial-geography/spatial-types-geography.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [table](../../t-sql/data-types/table-transact-sql.md) 
    :::column-end:::
    :::column:::
         
    :::column-end:::
:::row-end:::

  
## <a name="see-also"></a>참고 항목
[CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
[EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[함수&#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[LIKE&#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[sp_droptype&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)  
[sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)  
[sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
  
  
