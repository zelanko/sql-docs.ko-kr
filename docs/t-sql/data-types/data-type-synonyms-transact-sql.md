---
title: "데이터 형식 동의어 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/23/2017
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
- data types [SQL Server], synonyms
- alternate names [SQL Server]
- synonyms [SQL Server], data types
ms.assetid: 390eef67-1a49-4185-a971-e07765be9717
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1d9b1da2bdc7084268740cd7de2580e64ee9698b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-synonyms-transact-sql"></a>데이터 형식 동의어 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

데이터 형식 동의어는 ISO 호환성을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함되었습니다. 다음 표에서는 동의어 및 동의어가 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식을 나열합니다.
  
|동의어|SQL Server 시스템 데이터 형식|  
|---|---|
|**Binary varying**|**varbinary**|  
|**다양 한 문자**|**varchar**|  
|**문자**|**char**|  
|**문자**|**char(1)**|  
|**문자 (**  *n*  **)**|**char(n)**|  
|**다양 한 문자 (**  *n*  **)**|**varchar(n)**|  
|**년 12 월**|**decimal**|  
|**배정밀도**|**float**|  
|**float**[**(***n***)**]에 대 한  *n*  1-7|**real**|  
|**float**[**(***n***)**]에 대 한  *n*  = 8 15|**float**|  
|**integer**|**int**|  
|**국가별 문자 (**  *n*  **)**|**nchar (n)**|  
|**national char (**  *n*  **)**|**nchar (n)**|  
|**다양 한 국가별 문자 (**  *n*  **)**|**nvarchar (n)**|  
|**다양 한 national char (**  *n*  **)**|**nvarchar (n)**|  
|**national 텍스트**|**ntext**|  
|**timestamp**|rowversion|  
  
데이터 형식 동의어는 CREATE TABLE, CREATE PROCEDURE 같은 데이터 정의 언어 (DDL) 문 해당 기본 데이터 형식 이름 대신 사용할 수 있습니다 또는 선언  *@variable* 합니다. 그러나 개체가 만들어진 후에는 동의어가 표시되지 않습니다. 개체가 만들어질 때 동의어에 연결된 기본 데이터 형식이 개체에 할당되기 때문입니다. 개체를 만든 문에 동의어가 지정되었다는 기록은 남지 않습니다.
  
결과 집합 열이나 식 등 원래 개체에서 파생된 모든 개체에는 기본 데이터 형식이 할당됩니다. 이로 인해 원래 개체와 파생된 모든 개체에서 수행되는 모든 후속 메타데이터 함수는 동의어가 아니라 기본 데이터 형식을 보고하게 됩니다. 이 동작은 같은 메타 데이터 작업으로 발생 **sp_help** 와 다른 시스템 저장 프로시저, 정보 스키마 뷰 또는 테이블이 나 결과 집합의 데이터 형식을 보고 하는 다양 한 데이터 액세스 API 메타 데이터 작업 열입니다.
  
예를 들어 다음과 같이 `national character varying`을 지정하여 테이블을 만들 수 있습니다.
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol`실제로 할당는 **nvarchar (10)** 데이터 형식 및 모든 후속 메타 데이터 함수는 열으로 보고는 **nvarchar (10)** 열입니다. 메타 데이터 함수는으로 보고 하지 않습니다는 **국가별 문자 varying(10)** 열입니다.
  
## <a name="see-also"></a>참고 항목
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

