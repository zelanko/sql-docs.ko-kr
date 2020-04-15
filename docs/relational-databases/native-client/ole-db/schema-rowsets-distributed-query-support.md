---
title: 스키마 행 집합에서 분산 쿼리 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: daf4f4c0c7c6c1d53c2ab899dd150756399d53a3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297000"
---
# <a name="schema-rowsets---distributed-query-support"></a>스키마 행 집합 - 분산 쿼리 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  분산 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 쿼리를 지원하기 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 위해 네이티브 클라이언트 OLE DB 공급자 **IDBSchemaRowset** 인터페이스는 연결된 서버에서 메타데이터를 반환합니다.  
  
 DBPROPSET_SQLSERVERSESSION 속성 SSPROP_QUOTEDCATALOGNAMES가 VARIANT_TRUE이면 카탈로그 이름에 따옴표 붙은 식별자(예: "my.catalog")를 지정할 수 있습니다. 카탈로그별로 스키마 행 집합 출력을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 제한할 때 네이티브 클라이언트 OLE DB 공급자는 연결된 서버 및 카탈로그 이름을 포함하는 두 부분으로 구성된 이름을 인식합니다. 아래 표의 스키마 행 집합의 경우 두 부분으로 구성된 카탈로그 이름을 _linked_server._**.** _카탈로그는_ 명명된 연결된 서버의 해당 카탈로그로 출력을 제한합니다.  
  
|스키마 행 집합|카탈로그 제한|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMNS|TABLE_CATALOG|  
|DBSCHEMA_PRIMARY_KEYS|TABLE_CATALOG|  
|DBSCHEMA_TABLES|TABLE_CATALOG|  
|DBSCHEMA_FOREIGN_KEYS|PK_TABLE_CATALOG FK_TABLE_CATALOG|  
|DBSCHEMA_INDEXES|TABLE_CATALOG|  
|DBSCHEMA_COLUMN_PRIVILEGES|TABLE_CATALOG|  
|DBSCHEMA_TABLE_PRIVILEGES|TABLE_CATALOG|  
  
> [!NOTE]  
>  스키마 행 집합을 연결된 서버의 모든 카탈로그로 제한하려면 구문 *linked_server*(여기서 마침표 구분 기호가 이름 사양에 포함됨)를 사용합니다. 이 구문은 카탈로그 이름 제한에 NULL을 지정하는 것과 같으며 연결된 서버가 카탈로그를 지원하지 않는 데이터 원본을 나타내는 경우에도 사용됩니다.  
  
 네이티브 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 연결된 서버로 등록된 OLE DB 데이터 원본 목록을 반환하는 스키마 행 집합 LINKEDSERVERS를 정의합니다.  
  
## <a name="see-also"></a>참고 항목  
 [레올 DB&#41;&#40;스키마 행셋 지원](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 행 집합&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
