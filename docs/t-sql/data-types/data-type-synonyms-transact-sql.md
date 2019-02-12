---
title: 데이터 형식 동의어(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], synonyms
- alternate names [SQL Server]
- synonyms [SQL Server], data types
ms.assetid: 390eef67-1a49-4185-a971-e07765be9717
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 74fe3be365919d61a7b32587f910f083cc5e846d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034214"
---
# <a name="data-type-synonyms-transact-sql"></a>데이터 형식 동의어(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

데이터 형식 동의어는 ISO 호환성을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함되었습니다. 다음 표에서는 동의어 및 동의어가 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식을 나열합니다.
  
|동의어|SQL Server 시스템 데이터 형식|  
|---|---|
|**binary varying**|**varbinary**|  
|**char varying**|**varchar**|  
|**character**|**char**|  
|**character**|**char(1)**|  
|**character(**_n_**)**|**char(n)**|  
|**character varying(**_n_**)**|**varchar(n)**|  
|**Dec**|**decimal**|  
|**Double precision**|**float**|  
|**float**[**(**_n_**)**] for _n_ = 1-7|**real**|  
|**float**[**(**_n_**)**] for _n_ = 8-15|**float**|  
|**integer**|**int**|  
|**national character(**_n_**)**|**nchar(n)**|  
|**national char(**_n_**)**|**nchar(n)**|  
|**national character varying(**_n_**)**|**nvarchar(n)**|  
|**national char varying(**_n_**)**|**nvarchar(n)**|  
|**national text**|**ntext**|  
|**timestamp**|rowversion|  
  
데이터 형식 동의어는 DDL(데이터 정의 언어) 문에서 해당 기본 데이터 형식 이름 대신 사용할 수 있습니다. 해당 문에는 CREATE TABLE, CREATE PROCEDURE 및 DECLARE *@variable*이 포함됩니다. 그러나 개체가 만들어진 후에는 동의어가 표시되지 않습니다. 개체가 만들어질 때 동의어에 연결된 기본 데이터 형식이 개체에 할당되기 때문입니다. 개체를 만든 문에 동의어가 지정되었다는 기록은 남지 않습니다.
  
결과 집합 열이나 식 등 원래 개체에서 파생된 개체에는 기본 데이터 형식이 할당됩니다. 원래 개체와 파생된 개체를 사용하는 모든 메타데이터 함수는 다음을 포함하여 동의어가 아니라 기본 데이터 형식을 보고하게 됩니다.

* 메타데이터 작업(예: **sp_help**) 및 기타 시스템 저장 프로시저,
* 정보 스키마 뷰 및
* 테이블 또는 결과 세트 열의 데이터 형식을 보고하는 데이터 액세스 API 메타데이터 작업.
  
예를 들어 다음과 같이 `national character varying`을 지정하여 테이블을 만들 수 있습니다.
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol`에는 **nvarchar(10)** 데이터 형식이 할당되며 모든 다음 메타데이터 함수는 해당 열을 **nvarchar(10)** 열로 보고합니다. 메타데이터 함수가 이 열을 **national character varying(10)** 열로 보고하는 경우는 없습니다.
  
## <a name="see-also"></a>관련 항목:
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
