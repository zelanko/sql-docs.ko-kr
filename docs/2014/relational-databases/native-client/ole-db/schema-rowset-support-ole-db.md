---
title: 스키마 행 집합 지원 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- SQL Server Native Client OLE DB provider, schema rowsets
- rowsets [OLE DB], schema
ms.assetid: a75b4b69-b095-4690-9b31-a2b32a67489e
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f37a7e25bf720ffa20e29b005e6022115583ac7f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413321"
---
# <a name="schema-rowset-support-ole-db"></a>스키마 행 집합 지원(OLE DB)
  합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서는 연결된 된 서버에서 스키마 정보를 반환을 처리할 때 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 분산 쿼리 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 동의어를 지원하기는 하지만 동의어의 메타데이터는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 반환하지 않습니다.  
  
 다음 표에 스키마 행 집합 목록 및에서 지원 되는 제한 열은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다.  
  
|스키마 행 집합|제한 열|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMN_PRIVILEGES|모든 제한 사항이 지원됩니다.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|DBSCHEMA_COLUMNS|모든 제한 사항이 지원됩니다.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME<br /><br /> 다음의 추가 열은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 관련됩니다.<br /><br /> -COLUMN_LCID. 데이터 정렬의 로캘 ID입니다. COLUMN_LCID는 Windows LCID 값과 같습니다.<br />-COLUMN_COMPFLAGS 비교 데이터 정렬에 대 한 지를 정의 합니다. 데이터 형식은 DBPROB_FINDCOMPAREOPS와 같습니다.<br />-COLUMN_SORTID는는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 정렬에 대 한 스타일을 정렬 합니다.<br />-COLUMN_TDSCOLLATION는는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 열의 데이터 정렬입니다.<br />-IS_COMPUTED. 그렇지 않은 경우 열이 계산된 열 및 VARIANT_FALSE 이면 VARIANT_TRUE입니다.|  
|DBSCHEMA_FOREIGN_KEYS|모든 제한 사항이 지원됩니다.<br /><br /> PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|DBSCHEMA_INDEXES|제한 사항 1, 2, 3 및 5가 지원됩니다.<br /><br /> TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TABLE_NAME|  
|DBSCHEMA_PRIMARY_KEYS|모든 제한 사항이 지원됩니다.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_PROCEDURE_PARAMETERS|모든 제한 사항이 지원됩니다.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|DBSCHEMA_PROCEDURES|제한 사항 1, 2 및 3이 지원됩니다.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME<br /><br /> DBSCHEMA_PROCEDURES는 현재 사용자가 실행할 수 있는 프로시저나 현재 사용자가 VIEW DEFINITION 권한을 부여받은 프로시저만 반환합니다.|  
|DBSCHEMA_PROVIDER_TYPES|모든 제한 사항이 지원됩니다.<br /><br /> DATA_TYPE BEST_MATCH|  
|DBSCHEMA_SCHEMATA|모든 제한 사항이 지원됩니다.<br /><br /> CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|DBSCHEMA_STATISTICS|모든 제한 사항이 지원됩니다.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_TABLE_CONSTRAINTS|모든 제한 사항이 지원됩니다.<br /><br /> CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|DBSCHEMA_TABLE_PRIVILEGES|모든 제한 사항이 지원됩니다.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|DBSCHEMA_TABLES|모든 제한 사항이 지원됩니다.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|DBSCHEMA_TABLES_INFO|모든 제한 사항이 지원됩니다.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
  
## <a name="in-this-section"></a>섹션 내용  
 [스키마 행 집합에서 분산 쿼리 지원](schema-rowsets-distributed-query-support.md)  
  
 [LINKEDSERVERS 행 집합 &#40;OLE DB&#41;](schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;OLE DB&#41;](sql-server-native-client-ole-db.md)   
 [사용자 정의 형식 사용](../features/using-user-defined-types.md)  
  
  
