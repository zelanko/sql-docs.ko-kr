---
title: 스파스 열 지원 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b286ba7bde145a9a3676f38f329a8efbd932a4cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667648"
---
# <a name="sparse-columns-support-ole-db"></a>스파스 열 지원(OLE DB)
  이 항목에서는 스파스 열에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 지원에 대해 설명합니다. 스파스 열에 대한 자세한 내용은 [Sparse Columns Support in SQL Server Native Client](../features/sparse-columns-support-in-sql-server-native-client.md)을 참조하십시오. 샘플은 [열 및 스파스 열의 카탈로그 메타데이터 표시 &#40;OLE DB&#41;](../../native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md)를 참조하세요.  
  
## <a name="ole-db-statement-metadata"></a>OLE DB 문 메타데이터  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]부터 새 DBCOLUMNFLAGS 플래그 값인 DBCOLUMNFLAGS_SS_ISCOLUMNSET을 사용할 수 있습니다. 이 값은 `column_set` 값인 열에 대해 설정해야 합니다. DBCOLUMNFLAGS 플래그를 통해 검색할 수 있습니다 합니다 *dwFlags* icolumnsrowset:: Getcolumnsrowset에서 반환 된 행 집합의 DBCOLUMN_FLAGS 열과 icolumnsinfo:: Getcolumnsinfo의 매개 변수입니다.  
  
## <a name="ole-db-catalog-metadata"></a>OLE DB 카탈로그 메타데이터  
 DBSCHEMA_COLUMNS에는 다음과 같은 두 개의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 특정 열이 새로 추가되었습니다.  
  
|열 이름|데이터 형식|값/설명|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|열이 스파스 열이면 VARIANT_TRUE 값을 갖고, 그렇지 않으면 VARIANT_FALSE 값을 갖습니다.|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|열이 스파스 `column_set` 열이면 VARIANT_TRUE 값을 갖고, 그렇지 않으면 VARIANT_FALSE 값을 갖습니다.|  
  
 또한 다음과 같은 두 개의 스키마 행 집합도 새로 추가되었습니다. 이러한 행 집합은 DBSCHEMA_COLUMNS와 구조가 동일하지만 다른 내용을 반환합니다. DBSCHEMA_COLUMNS_EXTENDED는 `column_set` 멤버 자격에 관계없이 모든 열을 반환하고 DBSCHEMA_SPARSE_COLUMN_SET은 스파스 `column_set`의 멤버인 열만 반환합니다.  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>OLE DB DataTypeCompatibility 동작  
 연결 문자열에 있는 `DataTypeCompatibility=80`은 다음과 같이 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 클라이언트에서와 동일하게 동작합니다.  
  
-   새 스키마 행 집합이 표시되지 않으며 스키마 행 집합의 행 집합에 이러한 행 집합에 대한 행이 없습니다.  
  
-   COLUMNS 행 집합의 새 열이 표시되지 않습니다.  
  
-   DBCOLUMNFLAGS_SS_ISCOLUMNSET이 `column_set` 열에 대해 설정되지 않습니다.  
  
-   DBCOMPUTEMODE_NOTCOMPUTED가 `column_set` 열에 대해 설정됩니다.  
  
## <a name="ole-db-support-for-sparse-columns"></a>스파스 열에 대한 OLE DB 지원  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서는 다음과 같은 OLE DB 인터페이스가 스파스 열을 지원하도록 수정되었습니다.  
  
|유형 또는 멤버 함수|Description|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|새 DBCOLUMNFLAGS 플래그 값인 DBCOLUMNFLAGS_SS_ISCOLUMNSET이에 대해 설정 되어 `column_set` 열에서 *dwFlags*합니다.<br /><br /> DBCOLUMNFLAGS_WRITE가 `column_set` 열에 대해 설정됩니다.|  
|IColumsRowset::GetColumnsRowset|새 DBCOLUMNFLAGS 플래그 값인 DBCOLUMNFLAGS_SS_ISCOLUMNSET이 DBCOLUMN_FLAGS의 `column_set` 열에 대해 설정됩니다.<br /><br /> DBCOLUMN_COMPUTEMODE가 `column_set` 열에 대해 DBCOMPUTEMODE_DYNAMIC으로 설정됩니다.|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS는 새 열 두 개를 반환합니다. SS_IS_COLUMN_SET과 ss_is_sparse를 반환 합니다.<br /><br /> DBSCHEMA_COLUMNS는 `column_set`의 멤버가 아닌 열만 반환합니다.<br /><br /> 두 개의 새로운 스키마 행 집합 추가 되었습니다. DBSCHEMA_COLUMNS_EXTENDED는의 스파스 여부에 관계 없이 모든 열을 반환 하는 것 `column_set` 멤버 자격. DBSCHEMA_SPARSE_COLUMN_SET은 `column_set`의 멤버인 열만 반환합니다. 이러한 새 행 집합은 DBSCHEMA_COLUMNS와 동일한 열과 제한 사항을 갖습니다.|  
|IDBSchemaRowset::GetSchemas|IDBSchemaRowset::GetSchemas에는 사용 가능한 스키마 행 집합 목록에 있는 새 행 집합, DBSCHEMA_COLUMNS_EXTENDED 및 DBSCHEMA_SPARSE_COLUMN_SET에 대한 GUID가 포함됩니다.|  
|ICommand::Execute|하는 경우 **선택 \* 에서** *테이블* 은 스파스의 멤버가 아닌 모든 열 반환 사용 `column_set`과 열의 모든 null이 아닌 값을 포함 하는 XML 열 스파스 멤버인 `column_set`있을 경우.|  
|IOpenRowset::OpenRowset|Iopenrowset:: Openrowset icommand:: Execute와 동일한 열을 사용 하 여 행 집합을 사용 하 여 반환 된 **선택 \***  동일한 테이블에 대 한 쿼리.|  
|ITableDefinition|스파스 열이나 `column_set` 열의 경우 이 인터페이스에 변경 사항이 없습니다. 스키마를 수정해야 하는 응용 프로그램에서는 적절한 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 직접 실행해야 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](sql-server-native-client-ole-db.md)  
  
  
