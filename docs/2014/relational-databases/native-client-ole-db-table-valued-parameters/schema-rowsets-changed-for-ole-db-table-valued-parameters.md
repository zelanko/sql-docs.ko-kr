---
title: OLE DB 테이블 반환 매개 변수에 대해 변경된 스키마 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
ms.assetid: 581e3ead-53db-44da-8718-f3fc4b5108f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff0086d6b8c724ef83575cde387217ad69549d56
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213852"
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters"></a>OLE DB 테이블 반환 매개 변수에 대해 변경된 스키마 행 집합
  다음은 테이블 반환 매개 변수를 지원하기 위해 변경 또는 추가된 스키마 행 집합입니다.  
  
|스키마 행 집합|Description|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|SS_TYPE_CATALOG_NAME 및 SS_TYPE_SCHEMANAME이라는 두 개의 새 열이 행 집합 끝에 추가되었습니다. 두 열은 이후 유형에 다시 사용될 수 있습니다. TYPE_NAME 및 LOCAL_TYPE_NAME 열에는 테이블 반환 매개 변수 TABLE 유형의 이름이 포함됩니다. 테이블 반환 매개 변수의 경우 DATA_TYPE 열에 값 DBTYPE_TABLE = 143이 포함됩니다.|  
|DBSCHEMA_TABLE_TYPES|이 행 집합은 테이블 반환 매개 변수를 지원하기 위해 추가되었습니다. 테이블 유형에 대해서만 메타데이터를 반환하고 테이블, 뷰 또는 동의어에 대해서는 반환하지 않는다는 점을 제외하고 DBSCHEMA_TABLES와 같습니다. TABLE_TYPE 열은 값 'TABLE TYPE'을 갖습니다.|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|이 행 집합은 테이블 반환 매개 변수를 지원하기 위해 추가되었습니다. 테이블 유형에 대해서만 기본 키 메타데이터를 반환하고 테이블에 대해서는 반환하지 않는다는 점을 제외하고 DBSCHEMA_PRIMARY_KEYS와 같습니다.|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|이 행 집합은 테이블 반환 매개 변수를 지원하기 위해 추가되었습니다. 테이블 유형에 대해서만 열 메타데이터를 반환하고 테이블, 뷰 또는 동의어에 대해서는 반환하지 않는다는 점을 제외하고 DBSCHEMA_COLUMNS와 같습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수&#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
