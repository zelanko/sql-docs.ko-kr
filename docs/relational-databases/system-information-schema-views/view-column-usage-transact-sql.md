---
description: VIEW_COLUMN_USAGE(Transact-SQL)
title: VIEW_COLUMN_USAGE (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- VIEW_COLUMN_USAGE
- VIEW_COLUMN_USAGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.VIEW_COLUMN_USAGE view
- VIEW_COLUMN_USAGE view
ms.assetid: fc0b3608-a7e8-4532-8215-32235d6670f1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ec9d1411280352e19a4d9f8af76004f23414615b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539251"
---
# <a name="view_column_usage-transact-sql"></a>VIEW_COLUMN_USAGE(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스에서 뷰 정의에 사용되는 각 열에 대해 한 행을 반환합니다. 이 정보 스키마 뷰는 현재 사용자가 사용 권한을 갖고 있는 개체에 대한 정보를 반환합니다.  
  
 이러한 뷰에서 정보를 검색 하려면 INFORMATION_SCHEMA의 정규화 된 이름을 지정 합니다 **.** _view_name_.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**VIEW_CATALOG**|**nvarchar (** 128 **)**|뷰 한정자입니다.|  
|**VIEW_SCHEMA**|**nvarchar (** 128 **)**|뷰가 포함된 스키마의 이름입니다.<br /><br /> **&#42;&#42; 중요 한 것 **  은 개체의 스키마를 찾는 신뢰할 수 있는 방법 으로만 &#42;&#42;하 여 개체의 카탈로그 뷰를 쿼리 하는 것입니다.|  
|**VIEW_NAME**|**sysname**|뷰 이름입니다.|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|테이블 한정자입니다.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|테이블이 포함된 스키마의 이름입니다.<br /><br /> **&#42;&#42; 중요 한 것 **  은 개체의 스키마를 찾는 신뢰할 수 있는 방법 으로만 &#42;&#42;하 여 개체의 카탈로그 뷰를 쿼리 하는 것입니다.|  
|**TABLE_NAME**|**sysname**|기본 테이블입니다.|  
|**COLUMN_NAME**|**sysname**|열 이름입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰 ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Transact-sql&#41;&#40;정보 스키마 뷰 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sql_dependencies &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
