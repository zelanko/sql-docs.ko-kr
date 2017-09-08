---
title: SCHEMA_ID (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCHEMA_ID
- SCHEMA_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], schemas
- schemas [SQL Server], IDs
- SCHEMA_ID function
- IDs [SQL Server], schemas
- default schema IDs
ms.assetid: c8e34df5-3eea-459f-ae40-050909ce9fda
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e364abf5b75159600715be0a4823ba8fce847e2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="schemaid-transact-sql"></a>SCHEMA_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  스키마 이름과 연결된 스키마 ID를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SCHEMA_ID ( [ schema_name ] )   
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|----------|----------------|  
|*schema_name*|스키마 이름입니다. *schema_name* 는 **sysname**합니다. 경우 *schema_name* 를 지정 하지 않으면 SCHEMA_ID는 호출자의 기본 스키마의 ID가 반환 됩니다.|  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
 경우 NULL이 반환 됩니다 *schema_name* 유효한 스키마가 아닙니다.  
  
## <a name="remarks"></a>주의  
 SCHEMA_ID는 시스템 스키마 및 사용자 정의 스키마의 ID를 반환합니다. SCHEMA_ID는 선택 목록, WHERE 절 및 식이 사용되는 어디서나 호출할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>1. 호출자의 기본 스키마 ID 반환  
  
```  
SELECT SCHEMA_ID();  
GO  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>2. 명명된 스키마의 스키마 ID 반환  
  
```  
USE AdventureWorks2012;  
GO  
SELECT SCHEMA_ID('HumanResources');  
GO   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-the-default-schema-id-of-a-caller"></a>3. 호출자의 기본 스키마 ID 반환  
  
```  
SELECT SCHEMA_ID();  
```  
  
### <a name="d-returning-the-schema-id-of-a-named-schema"></a>4. 명명된 스키마의 스키마 ID 반환  
  
```  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME &#40; Transact SQL &#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys.schemas &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  


