---
title: sql_variant (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql_variant
- sql_variant_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sql_variant comparisons
- storing data [SQL Server], sql_variant
- sql_variant data type
- storage [SQL Server], sql_variant
ms.assetid: 01229779-8bc1-4c7d-890a-8246d4899250
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4eb946d5b6ed5a9c6d33789166327bd2dd25d7c1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="sqlvariant-transact-sql"></a>sql_variant(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원하는 여러 가지 데이터 형식의 값을 저장하는 데이터 형식입니다.
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)),[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
sql_variant  
```  
  
## <a name="remarks"></a>주의  
**sql_variant** 열, 매개 변수, 변수 및 사용자 정의 함수의 반환 값에서 사용할 수 있습니다. **sql_variant** 다른 데이터 형식의 값을 지 원하는 데 이러한 데이터베이스 개체를 사용 하도록 설정 합니다.
  
형식의 열 **sql_variant** 서로 다른 데이터 형식의 행이 포함 될 수 있습니다. 로 정의 된 열의 예를 들어 **sql_variant** 저장할 수 있는 **int**, **이진**, 및 **char** 값입니다.
  
**sql_variant** 8016 바이트의 최대 길이 가질 수 있습니다. 여기에는 기본 유형 정보 및 기본 유형 값이 모두 포함됩니다. 실제 기본 유형 값의 최대 길이는 8,000바이트입니다.
  
A **sql_variant** 데이터 형식 캐스트 되어야 해당 기본 데이터 형식 값에 더하기 및 빼기와 같은 작업에 사용 되기 전에 합니다.
  
**sql_variant** 기본값을 할당할 수 있습니다. 이 데이터 형식은 NULL을 기초값으로 가질 수는 있지만 NULL 값은 연결된 기본 유형을 갖지 않습니다. 또한 **sql_variant** 다른 없는 **sql_variant** 기본 형식으로.
  
고유, 기본 또는 외래 키 형식의 열을 포함할 수 **sql_variant**, 있지만 특정 행의 키를 구성 하는 데이터 값의 총 길이 인덱스의 최대 길이 초과 합니다. 크면 안 됩니다.
  
테이블이 개수에 관계 없이 포함할 수 **sql_variant** 열입니다.
  
**sql_variant** CONTAINSTABLE 및 FREETEXTTABLE에 사용할 수 없습니다.
  
ODBC 완전히 지원 하지 않는 **sql_variant**합니다. 따라서 쿼리가 **sql_variant** Microsoft OLE DB Provider for ODBC (MSDASQL)를 사용 하는 경우 열이 이진 데이터로 반환 됩니다. 예를 들어 한 **sql_variant** 문자열 데이터 'p s 2091'를 포함 하는 열은 0x505332303931 반환 됩니다.
  
## <a name="comparing-sqlvariant-values"></a>sql_variant 값 비교  
**sql_variant** 데이터 형식 변환에 대 한 데이터 형식 계층 구조 목록의 맨 위에 속합니다. 에 대 한 **sql_variant** 비교는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 계층 구조 순서는 데이터 형식 패밀리로 그룹화 됩니다.
  
|데이터 형식 계층|데이터 형식 패밀리|  
|---|---|
|**sql_variant**|**sql_variant**|  
|**datetime2**|날짜 및 시간|  
|**datetimeoffset**|날짜 및 시간|  
|**datetime**|날짜 및 시간|  
|**smalldatetime**|날짜 및 시간|  
|**date**|날짜 및 시간|  
|**time**|날짜 및 시간|  
|**float**|근사치|  
|**real**|근사치|  
|**decimal**|정확한 수치|  
|**money**|정확한 수치|  
|**smallmoney**|정확한 수치|  
|**bigint**|정확한 수치|  
|**int**|정확한 수치|  
|**smallint**|정확한 수치|  
|**tinyint**|정확한 수치|  
|**bit**|정확한 수치|  
|**nvarchar**|유니코드|  
|**nchar**|유니코드|  
|**varchar**|유니코드|  
|**char**|유니코드|  
|**varbinary**|이진|  
|**binary**|이진|  
|**uniqueidentifier**|**고유 식별자**|  
  
에 다음 규칙이 적용 **sql_variant** 비교:
-   때 **sql_variant** 서로 다른 기본 데이터 형식의 값을 비교 하 고 기본 데이터 형식이 서로 다른 데이터 형식 패밀리, 계층 구조 차트에서 데이터 형식 패밀리의 더 높은 값 두 값 중 더 큰 것으로 간주 됩니다.  
-   때 **sql_variant** 서로 다른 기본 데이터 형식의 값을 비교 하 고 기본 데이터 형식은 동일한 데이터 형식 패밀리에 있는, 계층 구조 차트에서 기본 데이터 형식이 더 낮은 값은 다른 데이터 형식으로 암시적으로 변환 하 고 다음 비교 됩니다.  
-   때 **sql_variant** 의 값은 **char**, **varchar**, **nchar**, 또는 **nvarchar** 데이터 형식은 비교할 때 해당 데이터 정렬이 먼저 비교 됩니다 다음 기준에 따라: LCID, LCID 버전, 비교 플래그 및 정렬 id입니다. 이러한 조건은 각각 정수 값으로, 그리고 나열된 순서대로 비교됩니다. 이러한 모든 조건이 같다면 실제 문자열 값은 데이터 정렬에 따라 비교됩니다.  
  
## <a name="converting-sqlvariant-data"></a>sql_variant 데이터 변환  
처리 하는 경우는 **sql_variant** 데이터 형식을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다른 데이터 형식으로 된 개체의 암시적 변환을 지원는 **sql_variant** 유형입니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 암시적 변환을 지원 하지 않습니다 **sql_variant** 데이터를 다른 데이터 형식의 개체입니다.
  
## <a name="restrictions"></a>제한 사항  
다음 표에서 사용 하 여 저장할 수 없는 값의 유형은 **sql_variant**:
  
|||  
|-|-|  
|**varchar(max)**|**varbinary(max)**|  
|**nvarchar(max)**|**xml**|  
|**text**|**ntext**|  
|**image**|**rowversion** (**타임 스탬프**)|  
|**sql_variant**|**geography**|  
|**hierarchyid**|**geometry**|  
|사용자 정의 형식|**datetimeoffset**|  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[SQL_VARIANT_PROPERTY &#40; Transact SQL &#41;](../../t-sql/functions/sql-variant-property-transact-sql.md)
  
  

