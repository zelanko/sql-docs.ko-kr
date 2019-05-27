---
title: SCHEMA_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b3692f3c0bc1c09a5841fcff146ceb9f4489548c
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65945428"
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
|*schema_id*|스키마의 ID입니다. *schema_id*는 **int**입니다. *schema_id*가 정의되어 있지 않으면 SCHEMA_NAME은 호출자의 기본 스키마 이름을 반환합니다.|  
  
## <a name="return-types"></a>반환 형식  
 **sysname**  
  
 *schema_id*가 유효한 ID가 아니면 NULL을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SCHEMA_ID&#40;Transact-SQL&#41;](../../t-sql/functions/schema-id-transact-sql.md)   
 [sys,schemas&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

