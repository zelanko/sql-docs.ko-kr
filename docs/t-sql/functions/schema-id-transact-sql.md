---
title: SCHEMA_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d2672fc584f377e521ae4e291963aed8c16aa612
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43085926"
---
# <a name="schemaid-transact-sql"></a>SCHEMA_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  스키마 이름과 연결된 스키마 ID를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SCHEMA_ID ( [ schema_name ] )   
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|----------|----------------|  
|*schema_name*|스키마 이름입니다. *schema_name*은 **sysname**입니다. *schema_name*을 지정하지 않으면 SCHEMA_ID는 호출자의 기본 스키마 ID를 반환합니다.|  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
 *schema_name*이 유효한 스키마가 아닌 경우 NULL이 반환됩니다.  
  
## <a name="remarks"></a>Remarks  
 SCHEMA_ID는 시스템 스키마 및 사용자 정의 스키마의 ID를 반환합니다. SCHEMA_ID는 선택 목록, WHERE 절 및 식이 사용되는 어디서나 호출할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>1. 호출자의 기본 스키마 ID 반환  
  
```  
SELECT SCHEMA_ID();  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>2. 명명된 스키마의 스키마 ID 반환  
  
```  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>참고 항목  
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  

