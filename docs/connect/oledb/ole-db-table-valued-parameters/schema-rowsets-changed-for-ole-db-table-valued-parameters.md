---
title: OLE DB 테이블 반환 매개 변수에 대 한 스키마 행 집합 변경 | Microsoft Docs
description: OLE DB Table-Valued 매개 변수에 대 한 변경 된 스키마 행 집합
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 6eb387969549f0ed72e3635a80fcd6db34852c10
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689836"
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters"></a>OLE DB 테이블 반환 매개 변수에 대해 변경된 스키마 행 집합
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  다음은 테이블 반환 매개 변수를 지원하기 위해 변경 또는 추가된 스키마 행 집합입니다.  
  
|스키마 행 집합|Description|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|SS_TYPE_CATALOG_NAME 및 SS_TYPE_SCHEMANAME이라는 두 개의 새 열이 행 집합 끝에 추가되었습니다. 두 열은 이후 유형에 다시 사용될 수 있습니다. TYPE_NAME 및 LOCAL_TYPE_NAME 열에는 테이블 반환 매개 변수 TABLE 유형의 이름이 포함됩니다. 테이블 반환 매개 변수의 경우 DATA_TYPE 열에 값 DBTYPE_TABLE = 143이 포함됩니다.|  
|DBSCHEMA_TABLE_TYPES|이 행 집합은 테이블 반환 매개 변수를 지원하기 위해 추가되었습니다. 테이블 유형에 대해서만 메타데이터를 반환하고 테이블, 뷰 또는 동의어에 대해서는 반환하지 않는다는 점을 제외하고 DBSCHEMA_TABLES와 같습니다. TABLE_TYPE 열은 값 'TABLE TYPE'을 갖습니다.|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|이 행 집합은 테이블 반환 매개 변수를 지원하기 위해 추가되었습니다. 테이블 유형에 대해서만 기본 키 메타데이터를 반환하고 테이블에 대해서는 반환하지 않는다는 점을 제외하고 DBSCHEMA_PRIMARY_KEYS와 같습니다.|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|이 행 집합은 테이블 반환 매개 변수를 지원하기 위해 추가되었습니다. 테이블 유형에 대해서만 열 메타데이터를 반환하고 테이블, 뷰 또는 동의어에 대해서는 반환하지 않는다는 점을 제외하고 DBSCHEMA_COLUMNS와 같습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수 &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수를 사용 하 여 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
