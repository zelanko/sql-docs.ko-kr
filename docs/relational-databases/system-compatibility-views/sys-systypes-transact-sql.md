---
title: sys.sys형식 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.systypes_TSQL
- systypes_TSQL
- sys.systypes
- systypes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.systypes compatibility view
- systypes system table
ms.assetid: 1b0b1d0c-5f7b-470b-bd52-8bfa922d7889
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4f0e341c069b1ce7e095e5ee8e17c098f21fd088
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85987094"
---
# <a name="syssystypes-transact-sql"></a>sys.systypes(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  데이터베이스에 정의된 각 시스템 제공 및 각 사용자 정의 데이터 형식당 하나의 행을 반환합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|데이터 형식의 이름입니다.|  
|**xtype**|**tinyint**|물리적 스토리지 유형입니다.|  
|**status**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**smallint**|확장 사용자 유형입니다. 데이터 형식 수가 32,767을 초과하면 오버플로되거나 NULL을 반환합니다.|  
|**length**|**smallint**|데이터 형식의 물리적 길이입니다.|  
|**xprec**|**tinyint**|서버에서 사용하는 내부적인 전체 자릿수입니다. 쿼리에서는 사용하지 않습니다.|  
|**xscale**|**tinyint**|서버에서 사용하는 내부적인 소수 자릿수입니다. 쿼리에서는 사용하지 않습니다.|  
|**tdefault**|**int**|해당 데이터 형식에 대한 무결성 검사를 포함하는 저장 프로시저의 ID입니다.|  
|**도메인**|**int**|해당 데이터 형식에 대한 무결성 검사를 포함하는 저장 프로시저의 ID입니다.|  
|**uid**|**smallint**|형식 소유자의 스키마 ID입니다.<br /><br /> 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드한 데이터베이스의 경우 스키마 ID는 소유자의 사용자 ID와 동일합니다.<br /><br /> 중요 다음 DDL 문 중 하나를 사용 하는 경우sys.sys** \* 형식 대신에는 \* sys. types 카탈로그 뷰를 사용 해야 합니다. \* \* ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) **sys.systypes**<br /><br /> ALTER AUTHORIZATION ON TYPE<br /><br /> CREATE TYPE<br /><br /> 사용자 및 역할 수가 32,767을 초과하는 경우 오버플로되거나 NULL을 반환합니다.|  
|**쓰이는**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**collationid**|**int**|Character based 인 경우 **collationid** 는 현재 데이터베이스의 데이터 정렬 id입니다. 그렇지 않으면 NULL입니다.|  
|**usertype**|**smallint**|사용자 유형 ID입니다. 데이터 형식 수가 32,767을 초과하면 오버플로되거나 NULL을 반환합니다.|  
|**변수**|**bit**|가변 길이 데이터 형식입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|**allownulls**|**bit**|해당 데이터 형식의 기본 NULL 허용 여부를 표시합니다. 이 기본값은 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 또는 [ALTER table](../../t-sql/statements/alter-table-transact-sql.md)을 사용 하 여 null 허용 여부를 지정 하는 경우에 의해 재정의 됩니다.|  
|**type**|**tinyint**|물리적인 스토리지 데이터 형식입니다.|  
|**printfmt**|**varchar(255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**smallint**|해당 데이터 형식에 대한 전체 자릿수 수준입니다.<br /><br /> -1 = **xml** 또는 대량 값 형식입니다.|  
|**scale**|**tinyint**|해당 데이터 형식의 소수 자릿수이며 전체 자릿수를 기반으로 합니다.<br /><br /> NULL = 데이터 형식이 숫자가 아닙니다.|  
|**부씩**|**sysname**|Character based 인 경우 **데이터 정렬은** 현재 데이터베이스의 데이터 정렬입니다. 그렇지 않으면 NULL입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;호환성 뷰](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
