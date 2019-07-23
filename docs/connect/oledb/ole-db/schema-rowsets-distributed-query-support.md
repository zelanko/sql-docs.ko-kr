---
title: 스키마 행 집합에서 분산 쿼리 지원 | Microsoft Docs
description: 스키마 행 집합에서 분산 쿼리 지원
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], OLE DB Driver for SQL Server
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 139186d64d2b7df6aca883a253e1f9fe3f062214
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993892"
---
# <a name="schema-rowsets---distributed-query-support"></a>스키마 행 집합 - 분산 쿼리 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 분산 쿼리를 지원하기 위해 SQL Server용 OLE DB 드라이버 **IDBSchemaRowset** 인터페이스는 연결된 서버에서 메타데이터를 반환합니다.  
  
 DBPROPSET_SQLSERVERSESSION 속성 SSPROP_QUOTEDCATALOGNAMES가 VARIANT_TRUE이면 카탈로그 이름에 따옴표 붙은 식별자(예: "my.catalog")를 지정할 수 있습니다. 스키마 행 집합 출력을 카탈로그별로 제한하면 SQL Server용 OLE DB 드라이버에서 연결된 서버와 카탈로그 이름이 포함된 두 부분으로 이루어진 이름을 인식합니다. 아래 표의 스키마 행 집합에 대해 두 부분으로 구성된 카탈로그 이름을 _linked\_server_ **.** _catalog_로 지정하면 명명된 연결된 서버에 적용 가능한 카탈로그로 출력이 제한됩니다.  
  
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
>  스키마 행 집합을 연결된 서버의 모든 카탈로그로 제한하려면 구문 *linked_server*(여기서 밑줄 구분 기호가 이름 사양에 포함됨)를 사용합니다. 이 구문은 카탈로그 이름 제한에 NULL을 지정하는 것과 같으며 연결된 서버가 카탈로그를 지원하지 않는 데이터 원본을 나타내는 경우에도 사용됩니다.  
 
 SQL Server용 OLE DB 드라이버는 연결된 서버로 등록된 OLE DB 데이터 원본 목록을 반환하는 스키마 행 집합 LINKEDSERVERS를 정의합니다.  
  
## <a name="see-also"></a>참고 항목  
 [스키마 행 집합 지원&#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 행 &#40;집합 OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
