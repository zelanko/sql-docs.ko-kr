---
title: SCHEMA_NAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCHEMA_NAME
- SCHEMA_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SCHEMA_NAME function
- schemas [SQL Server], names
ms.assetid: 20071b77-2b6e-4ce7-a8e3-fa71480baf73
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 41dd04ebbbc5b07512d243e5d4ac77761ba9ca1e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="schemaname-transact-sql"></a>SCHEMA_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  스키마 ID와 연관된 스키마 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SCHEMA_NAME ( [ schema_id ] )  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|----------|----------------|  
|*schema_id*|스키마의 ID입니다. *schema_id* 는 **int**합니다. 경우 *schema_id* 가 정의 되지 않은 SCHEMA_NAME 돌아갑니다 호출자의 기본 스키마의 이름입니다.|  
  
## <a name="return-types"></a>반환 형식  
 **sysname**  
  
 NULL을 반환 *schema_id* 유효한 ID가 아닙니다.  
  
## <a name="remarks"></a>주의  
 SCHEMA_NAME은 시스템 스키마와 사용자 정의 스키마의 이름을 반환합니다. SCHEMA_NAME은 SELECT 목록, WHERE 절 및 식을 사용할 수 있는 곳이면 어디에서나 호출할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-name-of-the-default-schema-of-the-caller"></a>1. 호출자의 기본 스키마 이름 반환  
  
```  
SELECT SCHEMA_NAME();  
```  
  
### <a name="b-returning-the-name-of-a-schema-by-using-an-id"></a>2. ID를 사용하여 스키마 이름 반환  
  
```  
SELECT SCHEMA_NAME(1);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SCHEMA_ID &#40; Transact SQL &#41;](../../t-sql/functions/schema-id-transact-sql.md)   
 [sys.schemas &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

