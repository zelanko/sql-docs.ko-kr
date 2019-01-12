---
title: SCHEMATA (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: da1a5a26b1d10dca107e7ba061f53ce416348f73
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129593"
---
# <a name="schemata-transact-sql"></a>SCHEMATA(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스 내의 각 스키마당 한 개의 행을 반환합니다. 이러한 뷰에서 정보를 검색할의 정규화 된 이름을 지정 **INFORMATION_SCHEMA.** _view_name_합니다. 인스턴스의 모든 데이터베이스에 대 한 정보를 검색할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 쿼리 합니다 [sys.databases &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|현재 데이터베이스의 이름입니다.|  
|**SCHEMA_NAME**|**nvarchar(** 128 **)**|스키마 이름을 반환합니다.|  
|**SCHEMA_OWNER**|**nvarchar(** 128 **)**|스키마 소유자의 이름입니다.<br /><br /> **&#42;&#42;중요 &#42; &#42;**  개체의 스키마를 확인 하려면 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. 신뢰할 수 있는 유일한 개체 스키마 검색 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|항상 NULL을 반환합니다.|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|항상 NULL을 반환합니다.|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|기본 문자 집합의 이름을 반환합니다.|  

**예제**  
다음 예제에서는 master 데이터베이스의 스키마에 대 한 정보를 반환 합니다.  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>관련 항목  
 [시스템 뷰 &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [정보 스키마 뷰 &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys,schemas&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.syscharsets &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
  
