---
title: 데이터 형식 동의어(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
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
ms.openlocfilehash: 482177b87fb4d62cbebb64361e0b26ed9a681c1f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816561"
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
|**character(** *n* **)**|**char(n)**|  
|**character varying(** *n* **)**|**varchar(n)**|  
|**Dec**|**decimal**|  
|**Double precision**|**float**|  
|**float**[**(***n***)**] for *n* = 1-7|**real**|  
|**float**[**(***n***)**] for *n* = 8-15|**float**|  
|**integer**|**int**|  
|**national character(** *n* **)**|**nchar(n)**|  
|**national char(** *n* **)**|**nchar(n)**|  
|**national character varying(** *n* **)**|**nvarchar(n)**|  
|**national char varying(** *n* **)**|**nvarchar(n)**|  
|**national text**|**ntext**|  
|**timestamp**|rowversion|  
  
데이터 형식 동의어는 CREATE TABLE, CREATE PROCEDURE, DECLARE *@variable* 등의 DDL(데이터 정의 언어) 문에서 해당 기본 데이터 형식 이름 대신 사용할 수 있습니다. 그러나 개체가 만들어진 후에는 동의어가 표시되지 않습니다. 개체가 만들어질 때 동의어에 연결된 기본 데이터 형식이 개체에 할당되기 때문입니다. 개체를 만든 문에 동의어가 지정되었다는 기록은 남지 않습니다.
  
결과 집합 열이나 식 등 원래 개체에서 파생된 모든 개체에는 기본 데이터 형식이 할당됩니다. 이로 인해 원래 개체와 파생된 모든 개체에서 수행되는 모든 후속 메타데이터 함수는 동의어가 아니라 기본 데이터 형식을 보고하게 됩니다. 이 동작은 **sp_help**와 그 밖의 시스템 저장 프로시저, 정보 스키마 뷰 또는 다양한 데이터 액세스 API 등 테이블이나 결과 집합 열의 데이터 형식을 보고하는 메타데이터 작업 시 나타납니다.
  
예를 들어 다음과 같이 `national character varying`을 지정하여 테이블을 만들 수 있습니다.
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol`에는 실제로 **nvarchar(10)** 데이터 형식이 할당되며 모든 후속 메타데이터 함수는 해당 열을 **nvarchar(10)** 열로 보고합니다. 메타데이터 함수가 이 열을 **national character varying(10)** 열로 보고하는 경우는 없습니다.
  
## <a name="see-also"></a>관련 항목:
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
