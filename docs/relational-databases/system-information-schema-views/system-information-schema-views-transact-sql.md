---
title: 시스템 정보 스키마 뷰 (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-information-schema-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- information schema views
- schemas [SQL Server], information schema views
- metadata [SQL Server], views
- views [SQL Server], information schema
- system views [SQL Server], information schema
ms.assetid: 7e9f1dfe-27e9-40e7-8fc7-bfc5cae6be10
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 13c8c27fc41e567bd7fab020b537a6d0b8d081f7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="system-information-schema-views-transact-sql"></a>시스템 정보 스키마 뷰 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  정보 스키마 뷰는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 메타데이터를 가져오기 위해 사용할 수 있는 여러 수단 중 하나입니다. 정보 스키마 뷰는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타데이터의 내부 시스템 테이블에 종속되지 않는 뷰를 제공합니다. 정보 스키마 뷰는 기본 시스템 테이블이 많이 변경되더라도 응용 프로그램이 제대로 작동할 수 있도록 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함된 정보 스키마 뷰는 INFORMATION_SCHEMA에 대한 ISO 표준 정의를 준수합니다.  
  
> [!IMPORTANT]  
>  정보 스키마 뷰는 일부 변경되어 이전 버전과 호환되지 않습니다. 이러한 변경 내용은 각 뷰에 해당하는 항목에서 설명합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 현재 서버를 참조할 때 세 부분으로 된 명명 규칙을 지원합니다. ISO 표준도 세 부분으로 된 명명 규칙을 지원합니다. 그러나 두 명명 규칙에 사용되는 이름은 서로 다릅니다. 정보 스키마 뷰는 INFORMATION_SCHEMA라는 특수한 스키마에 정의됩니다. 이 스키마는 각 데이터베이스에 있습니다. 각 정보 스키마 뷰에는 해당 특정 데이터베이스에 저장된 모든 데이터 개체에 대한 메타데이터가 들어 있습니다. 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이름과 SQL 표준 이름 간의 관계를 보여 줍니다.  
  
|SQL Server 이름|매핑되는 해당 SQL 표준 이름|  
|---------------------|-----------------------------------------------|  
|데이터베이스|Catalog|  
|스키마|스키마|  
|개체|개체|  
|사용자 정의 데이터 형식|도메인|  
  
 이 이름 매핑 규칙은 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ISO 호환 뷰에 적용됩니다.  
  
|||  
|-|-|  
|[CHECK_CONSTRAINTS](../../relational-databases/system-information-schema-views/check-constraints-transact-sql.md)|[REFERENTIAL_CONSTRAINTS](../../relational-databases/system-information-schema-views/referential-constraints-transact-sql.md)|  
|[COLUMN_DOMAIN_USAGE](../../relational-databases/system-information-schema-views/column-domain-usage-transact-sql.md)|[ROUTINES](../../relational-databases/system-information-schema-views/routines-transact-sql.md)|  
|[COLUMN_PRIVILEGES](../../relational-databases/system-information-schema-views/column-privileges-transact-sql.md)|[ROUTINE_COLUMNS](../../relational-databases/system-information-schema-views/routine-columns-transact-sql.md)|  
|[COLUMNS](../../relational-databases/system-information-schema-views/columns-transact-sql.md)|[SCHEMATA](../../relational-databases/system-information-schema-views/schemata-transact-sql.md)|  
|[CONSTRAINT_COLUMN_USAGE](../../relational-databases/system-information-schema-views/constraint-column-usage-transact-sql.md)|[TABLE_CONSTRAINTS](../../relational-databases/system-information-schema-views/table-constraints-transact-sql.md)|  
|[CONSTRAINT_TABLE_USAGE](../../relational-databases/system-information-schema-views/constraint-table-usage-transact-sql.md)|[TABLE_PRIVILEGES](../../relational-databases/system-information-schema-views/table-privileges-transact-sql.md)|  
|[DOMAIN_CONSTRAINTS](../../relational-databases/system-information-schema-views/domain-constraints-transact-sql.md)|[TABLES](../../relational-databases/system-information-schema-views/tables-transact-sql.md)|  
|[DOMAINS](../../relational-databases/system-information-schema-views/domains-transact-sql.md)|[VIEW_COLUMN_USAGE](../../relational-databases/system-information-schema-views/view-column-usage-transact-sql.md)|  
|[KEY_COLUMN_USAGE](../../relational-databases/system-information-schema-views/key-column-usage-transact-sql.md)|[VIEW_TABLE_USAGE](../../relational-databases/system-information-schema-views/view-table-usage-transact-sql.md)|  
|[PARAMETERS](../../relational-databases/system-information-schema-views/parameters-transact-sql.md)|[VIEWS](../../relational-databases/system-information-schema-views/views-transact-sql.md)|  
  
 또한 일부 뷰는 문자 데이터 또는 이진 데이터 등의 다른 클래스의 데이터에 대한 참조를 포함합니다.  
  
 정보 스키마 뷰를 참조할 경우 `INFORMATION_SCHEMA` 스키마 이름이 포함된 정규화된 이름을 사용해야 합니다. 예를 들어:  
  
```  
SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = N'Product';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
