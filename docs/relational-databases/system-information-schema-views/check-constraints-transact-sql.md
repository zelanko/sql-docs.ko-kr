---
title: CHECK_CONSTRAINTS (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHECK_CONSTRAINTS
- CHECK_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHECK_CONSTRAINTS view
- INFORMATION_SCHEMA.CHECK_CONSTRAINTS view
ms.assetid: e9577fd2-c349-4dff-874c-9e57d2e5a3ec
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b156b8220bd0c8acdf6ff20e60b6dc4a147a1fc3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810241"
---
# <a name="checkconstraints-transact-sql"></a>CHECK_CONSTRAINTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스의 각 CHECK 제약 조건에 대해 한 행씩 반환합니다. 이 정보 스키마 뷰는 현재 사용자가 사용 권한을 갖고 있는 개체에 대한 정보를 반환합니다.  
  
 이러한 뷰에서 정보를 검색할의 정규화 된 이름을 지정 **INFORMATION_SCHEMA. * * * view_name*합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|제약 조건 한정자입니다.|  
|**CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|제약 조건이 속한 스키마의 이름입니다.<br /><br /> **\*\* 중요 \* \***  개체의 스키마를 확인 하려면 INFORMATION_SCHEMA 뷰를 사용 하지 마십시오. 개체의 스키마를 확인하는 신뢰할 수 있는 유일한 방법은 sys.objects 카탈로그 뷰를 쿼리하는 것입니다.|  
|**제약 조건 이름**|**sysname**|제약 조건 이름입니다.|  
|**CHECK_CLAUSE**|**nvarchar (** 4000 **)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 정의 문의 실제 텍스트입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 뷰 &#40;TRANSACT-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [정보 스키마 뷰 &#40;TRANSACT-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.check_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
