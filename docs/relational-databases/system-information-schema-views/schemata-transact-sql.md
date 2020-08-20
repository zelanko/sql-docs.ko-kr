---
description: SCHEMATA(Transact-SQL)
title: SCHEMATA (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SCHEMATA_TSQL
- SCHEMATA
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
- SCHEMATA view
ms.assetid: 69617642-0f54-4b25-b62f-5f39c8909601
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c9ebda1788cf5a06b034a38734e7a8cb6bb4e262
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481741"
---
# <a name="schemata-transact-sql"></a>SCHEMATA(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스 내의 각 스키마당 한 개의 행을 반환합니다. 이러한 뷰에서 정보를 검색 하려면 INFORMATION_SCHEMA의 정규화 된 이름을 지정 합니다 **.** _view_name_. 인스턴스의 모든 데이터베이스에 대 한 정보를 검색 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰를 쿼리 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|현재 데이터베이스의 이름입니다.|  
|**SCHEMA_NAME**|**nvarchar (** 128 **)**|스키마 이름을 반환합니다.|  
|**SCHEMA_OWNER**|**nvarchar (** 128 **)**|스키마 소유자의 이름입니다.<br /><br /> **&#42;&#42; 중요 &#42;&#42;** INFORMATION_SCHEMA 뷰를 사용 하 여 개체의 스키마를 확인 하지 마십시오. INFORMATION_SCHEMA 뷰는 개체의 메타 데이터 하위 집합만을 나타냅니다. 신뢰할 수 있는 유일한 개체 스키마 검색 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|항상 NULL을 반환합니다.|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|항상 NULL을 반환합니다.|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|기본 문자 집합의 이름을 반환합니다.|  

**예제**  
다음 예에서는 master 데이터베이스의 스키마에 대 한 정보를 반환 합니다.  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰 ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Transact-sql&#41;&#40;정보 스키마 뷰 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys,schemas&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.sys문자 집합 &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
  
