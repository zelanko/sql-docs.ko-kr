---
description: TABLES(Transact-SQL)
title: TABLES (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 05/20/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- TABLES_TSQL
- TABLES
dev_langs:
- TSQL
helpviewer_keywords:
- TABLES view
- INFORMATION_SCHEMA.TABLES view
ms.assetid: 723a9e63-8f6e-4d6e-b570-468cfaf03201
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d2879f58b53be571be8527ace6c4a7340e700f0d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550150"
---
# <a name="tables-transact-sql"></a>TABLES(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 사용자에 게 사용 권한이 있는 현재 데이터베이스의 각 테이블 또는 뷰에 대해 하나의 행을 반환 합니다.  
  
 이러한 뷰에서 정보를 검색 하려면 INFORMATION_SCHEMA의 정규화 된 이름을 지정 합니다 **.** _view_name_.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|테이블 한정자입니다.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|테이블이 포함된 스키마의 이름입니다.<br /><br /> <strong> \* \* 중요 \* \* </strong> 개체의 스키마를 확인 하는 것은 신뢰할 수 있는 유일한 방법입니다. INFORMATION_SCHEMA 뷰는 모든 새 기능을 반영하도록 업데이트되지 않으므로 완전하지 않을 수 있습니다.|  
|**TABLE_NAME**|**sysname**|테이블 또는 뷰 이름입니다.|  
|**TABLE_TYPE**|**varchar (** 10 **)**|테이블 유형입니다. VIEW 또는 BASE TABLE이 될 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰 ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Transact-sql&#41;&#40;정보 스키마 뷰 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)  
  
  
