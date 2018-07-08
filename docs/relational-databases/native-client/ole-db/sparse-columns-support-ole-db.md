---
title: 스파스 열 지원 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 25e45c61290a45240d5e4595a015b543ed89db29
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409102"
---
# <a name="sparse-columns-support-ole-db"></a>스파스 열 지원(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  이 항목에서는 스파스 열에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 지원에 대해 설명합니다. 스파스 열에 대한 자세한 내용은 [Sparse Columns Support in SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)을 참조하십시오. 샘플을 보려면 [표시 열 및 스파스 열의 카탈로그 메타 데이터 &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md)합니다.  
  
## <a name="ole-db-statement-metadata"></a>OLE DB 문 메타데이터  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]부터 새 DBCOLUMNFLAGS 플래그 값인 DBCOLUMNFLAGS_SS_ISCOLUMNSET을 사용할 수 있습니다. 이 값에 대 한 설정 해야 **column_set** 값입니다. DBCOLUMNFLAGS 플래그를 통해 검색할 수 있습니다 합니다 *dwFlags* icolumnsrowset:: Getcolumnsrowset에서 반환 된 행 집합의 DBCOLUMN_FLAGS 열과 icolumnsinfo:: Getcolumnsinfo의 매개 변수입니다.  
  
## <a name="ole-db-catalog-metadata"></a>OLE DB 카탈로그 메타데이터  
 DBSCHEMA_COLUMNS에는 다음과 같은 두 개의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 특정 열이 새로 추가되었습니다.  
  
|열 이름|데이터 형식|값/설명|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|열이 스파스 열이면 VARIANT_TRUE 값을 갖고, 그렇지 않으면 VARIANT_FALSE 값을 갖습니다.|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|열이 스파스 **column_set** 열에 VARIANT_TRUE 값이이 고, 그렇지 않으면 VARIANT_FALSE입니다.|  
  
 또한 다음과 같은 두 개의 스키마 행 집합도 새로 추가되었습니다. 이러한 행 집합은 DBSCHEMA_COLUMNS와 구조가 동일하지만 다른 내용을 반환합니다. DBSCHEMA_COLUMNS_EXTENDED에 관계 없이 모든 열을 반환 **column_set** 멤버 자격. Dbschema_sparse_column_set은 스파스의 멤버인 열만 반환 **column_set**합니다.  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>OLE DB DataTypeCompatibility 동작  
 동작 **DataTypeCompatibility = 80** (연결 문자열)은 일치 하는 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 같이 클라이언트:  
  
-   새 스키마 행 집합이 표시되지 않으며 스키마 행 집합의 행 집합에 이러한 행 집합에 대한 행이 없습니다.  
  
-   COLUMNS 행 집합의 새 열이 표시되지 않습니다.  
  
-   DBCOLUMNFLAGS_SS_ISCOLUMNSET 설정 되지 않습니다 **column_set** 열입니다.  
  
-   에 대해 설정 된 DBCOMPUTEMODE_NOTCOMPUTED **column_set** 열입니다.  
  
## <a name="ole-db-support-for-sparse-columns"></a>스파스 열에 대한 OLE DB 지원  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서는 다음과 같은 OLE DB 인터페이스가 스파스 열을 지원하도록 수정되었습니다.  
  
|유형 또는 멤버 함수|Description|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|새 DBCOLUMNFLAGS 플래그 값인 DBCOLUMNFLAGS_SS_ISCOLUMNSET이에 대해 설정 되어 **column_set** 열에서 *dwFlags*합니다.<br /><br /> 에 대해 설정 된 DBCOLUMNFLAGS_WRITE **column_set** 열입니다.|  
|IColumsRowset::GetColumnsRowset|에 새 DBCOLUMNFLAGS 플래그 값인 dbcolumnflags_ss_iscolumnset이 설정 되어 **column_set** DBCOLUMN_FLAGS의 열입니다.<br /><br /> DBCOLUMN_COMPUTEMODE에 DBCOMPUTEMODE_DYNAMIC로 설정 되어 **column_set** 열입니다.|  
|IDBSchemaRowset::GetSchemaRowset|Dbschema_columns는 두 개의 새 열: SS_IS_COLUMN_SET과 ss_is_sparse를 반환 합니다.<br /><br /> DBSCHEMA_COLUMNS의 멤버가 아닌 열만 반환 된 **column_set**합니다.<br /><br /> 두 개의 새로운 스키마 행 집합을 추가한: DBSCHEMA_COLUMNS_EXTENDED는의 스파스 여부에 관계 없이 모든 열을 반환 하는 것 **column_set** 멤버 자격. Dbschema_sparse_column_set은의 멤버인 열만 반환 된 **column_set**합니다. 이러한 새 행 집합은 DBSCHEMA_COLUMNS와 동일한 열과 제한 사항을 갖습니다.|  
|IDBSchemaRowset::GetSchemas|Idbschemarowset:: Getschemas 사용 가능한 스키마 행 집합의 목록에 새 행 집합, DBSCHEMA_COLUMNS_EXTENDED 및 DBSCHEMA_SPARSE_COLUMN_SET에 대 한 Guid를 포함합니다.|  
|ICommand::Execute|하는 경우 **선택 \* 에서** *테이블* 은 스파스의 멤버가 아닌 모든 열 반환 사용 **column_set**, 모든 값이 포함 된 XML 열 또한 null이 아닌 열을 스파스 멤버인 **column_set**있을 경우.|  
|IOpenRowset::OpenRowset|Iopenrowset:: Openrowset icommand:: Execute와 동일한 열을 사용 하 여 행 집합을 사용 하 여 반환 된 **선택 \***  동일한 테이블에 대 한 쿼리.|  
|ITableDefinition|이 인터페이스 또는 스파스 열에 대 한 변경 사항이 없는 **column_set** 열입니다. 스키마를 수정해야 하는 응용 프로그램에서는 적절한 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 직접 실행해야 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
