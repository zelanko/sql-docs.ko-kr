---
description: SQL Server Native Client에서 스키마 행 집합 지원 (OLE DB)
title: 스키마 행 집합 지원(OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- SQL Server Native Client OLE DB provider, schema rowsets
- rowsets [OLE DB], schema
ms.assetid: a75b4b69-b095-4690-9b31-a2b32a67489e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 60d49b2a2709560c17ac42ec78fd047326e420a2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467584"
---
# <a name="schema-rowset-support-in-sql-server-native-client-ole-db"></a>SQL Server Native Client에서 스키마 행 집합 지원 (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 분산 쿼리를 처리할 때 연결 된 서버에서 스키마 정보를 반환 하는 것도 지원 합니다 [!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 동의어를 지원하기는 하지만 동의어의 메타데이터는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 반환하지 않습니다.  
  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 지 원하는 스키마 행 집합 및 제한 열을 나열 합니다.  
  
|스키마 행 집합|제한 열|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMN_PRIVILEGES|모든 제한 사항이 지원됩니다.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|DBSCHEMA_COLUMNS|모든 제한 사항이 지원됩니다.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME<br /><br /> 다음의 추가 열은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 관련됩니다.<br /><br /> COLUMN_LCID. 데이터 정렬의 로캘 ID입니다. COLUMN_LCID는 Windows LCID 값과 같습니다.<br /><br /> COLUMN_COMPFLAGS. 데이터 정렬에 지원되는 비교를 정의합니다. 데이터 형식은 DBPROB_FINDCOMPAREOPS와 같습니다.<br /><br /> COLUMN_SORTID. 데이터 정렬에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 정렬 스타일입니다.<br /><br /> COLUMN_TDSCOLLATION. 열에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 정렬입니다.<br /><br /> IS_COMPUTED. 열이 계산 열이면 VARIANT_TRUE이고, 그렇지 않으면 VARIANT_FALSE입니다.|  
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
 [스키마 행 집합에서 분산 쿼리 지원](../../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md)  
  
 [LINKEDSERVERS 행 집합&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [사용자 정의 형식 사용](../../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
