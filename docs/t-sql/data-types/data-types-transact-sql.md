---
title: "데이터 형식 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 9/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system data types [SQL Server]
- data types [SQL Server]
- data types [SQL Server], about data types
ms.assetid: a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: d9a995f7d29fe91e14affa9266a9bce73acc9010
ms.openlocfilehash: 75efc7b5a58b3739a196e36b2c80d4ee37a92003
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="data-types-transact-sql"></a>데이터 형식 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 각 열, 지역 변수, 식 및 매개 변수는 관련된 데이터 형식을 가집니다. 데이터 형식은 개체가 보유할 수 있는 정수 데이터, 문자 데이터, 통화 데이터, 날짜 및 시간 데이터, 이진 문자열 등의 데이터 형식을 지정하는 특성입니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 있는 모든 데이터 형식을 정의하는 일련의 시스템 데이터 형식을 제공합니다. 사용자 지정 데이터 형식에 정의할 수도 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]합니다. 별칭 데이터 형식은 시스템이 제공하는 데이터 형식을 기반으로 합니다. 별칭 데이터 형식에 대 한 자세한 내용은 참조 하세요. [CREATE type&#40; Transact SQL &#41; ](../../t-sql/statements/create-type-transact-sql.md). 사용자 정의 형식의 특징은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에서 지원하는 프로그래밍 언어 중 하나로 만든 클래스의 메서드 및 연산자에서 가져옵니다.
  
데이터 형식, 데이터 정렬, 전체 자릿수, 소수 자릿수 또는 길이가 다른 두 식이 연산자에 의해 결합된 경우 그 특징은 다음 규칙에 따라 결정됩니다.
-   결합 결과의 데이터 형식은 입력 식의 데이터 형식에 데이터 형식 우선 순위 규칙을 적용하여 결정됩니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
-   결과 데이터 형식이 면 결과의 데이터 정렬 선행 정렬 우선 순위 규칙에 의해 결정 됩니다 **char**, **varchar**, **텍스트**, **nchar**, **nvarchar**, 또는 **ntext**합니다. 자세한 내용은 참조 [데이터 정렬 선행 규칙 &#40; Transact SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).  
-   결과의 전체 자릿수, 소수 자릿수 및 길이는 입력 식의 전체 자릿수, 소수 자릿수, 길이에 따라 달라집니다. 자세한 내용은 [전체 자릿수, 소수 자릿수 및 길이&#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)를 참조하세요.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ISO 호환성을 위해 데이터 형식 동의어를 제공합니다. 자세한 내용은 참조 [데이터 형식 동의어 &#40; Transact SQL &#41; ](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
## <a name="data-type-categories"></a>데이터 형식 범주
데이터 형식을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 범주로 구성 됩니다.
  
|||  
|-|-|  
|정확한 수치|유니코드 문자열|  
|근사치|이진 문자열|  
|날짜 및 시간|기타 데이터 형식|  
|문자열||  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 일부 데이터 형식은 저장 특징에 따라 다음 그룹에 속하도록 지정됩니다.
-   큰 값 데이터 형식: **varchar (max)**, 및 **nvarchar (max)**  
-   큰 개체 데이터 형식: **텍스트**, **ntext**, **이미지**, **varbinary (max)**, 및 **xml**  
  
    > [!NOTE]  
    >  sp_help는 큰 값에 대 한 길이로-1을 반환 하 고 **xml** 데이터 형식입니다.  
  
### <a name="exact-numerics"></a>정확한 수치
  
|||  
|-|-|  
|[bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[numeric](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[decimal](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|[smallmoney](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)||  
  
### <a name="approximate-numerics"></a>근사치
  
|||  
|-|-|  
|[float](../../t-sql/data-types/float-and-real-transact-sql.md)|[real](../../t-sql/data-types/float-and-real-transact-sql.md)|  
  
### <a name="date-and-time"></a>날짜 및 시간
  
|||  
|-|-|  
|[date](../../t-sql/data-types/date-transact-sql.md)|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|[time](../../t-sql/data-types/time-transact-sql.md)|  
  
### <a name="character-strings"></a>문자열
  
|||  
|-|-|  
|[char](../../t-sql/data-types/char-and-varchar-transact-sql.md)|[varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|[text](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="unicode-character-strings"></a>유니코드 문자열
  
|||  
|-|-|  
|[nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|[nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
|[ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="binary-strings"></a>이진 문자열
  
|||  
|-|-|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|[image](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="other-data-types"></a>기타 데이터 형식
  
|||  
|-|-|  
|[cursor](../../t-sql/data-types/cursor-transact-sql.md)|[rowversion](../../t-sql/data-types/rowversion-transact-sql.md)|  
|[hierarchyid](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md)|  
|[sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)|[xml](../../t-sql/xml/xml-transact-sql.md)|  
|[기 하 도형 공간 형식](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md) |[공간 지리 유형](../../t-sql/spatial-geography/spatial-types-geography.md)|  
|[table](../../t-sql/data-types/table-transact-sql.md) | |
  
## <a name="see-also"></a>참고 항목
[CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[선언 @local_variable &#40; Transact SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 
 [Execute&#40; Transact SQL &#41;](../../t-sql/language-elements/execute-transact-sql.md)  
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[함수 &#40; Transact SQL &#41;](../../t-sql/functions/functions.md)  
[마찬가지로 &#40; Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[sp_droptype &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)  
[sp_help&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)  
[sp_rename&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
  
  

