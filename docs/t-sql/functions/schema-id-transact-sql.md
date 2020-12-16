---
description: SCHEMA_ID(Transact-SQL)
title: SCHEMA_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 607290f62a358a370021f753f6bdcb2074f70131
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480414"
---
# <a name="schema_id-transact-sql"></a>SCHEMA_ID(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  스키마 이름과 연결된 스키마 ID를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
SCHEMA_ID ( [ schema_name ] )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
  
|용어|정의|  
|----------|----------------|  
|*schema_name*|스키마 이름입니다. *schema_name* 은 **sysname** 입니다. *schema_name* 을 지정하지 않으면 SCHEMA_ID는 호출자의 기본 스키마 ID를 반환합니다.|  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
 *schema_name* 이 유효한 스키마가 아닌 경우 NULL이 반환됩니다.  
  
## <a name="remarks"></a>설명  
 SCHEMA_ID는 시스템 스키마 및 사용자 정의 스키마의 ID를 반환합니다. SCHEMA_ID는 선택 목록, WHERE 절 및 식이 사용되는 어디서나 호출할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>A. 호출자의 기본 스키마 ID 반환  
  
```sql  
SELECT SCHEMA_ID();  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>B. 명명된 스키마의 스키마 ID 반환  
  
```sql  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>관련 항목  
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys,schemas&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  

