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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3c162bbcbf9f9212d6adc3838a06b5eaaac8b13
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73759706"
---
# <a name="schema-rowsets---distributed-query-support"></a>스키마 행 집합 - 분산 쿼리 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 분산 쿼리를 지원 하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB provider **IDBSchemaRowset** 인터페이스는 연결 된 서버에 대 한 메타 데이터를 반환 합니다.  
  
 DBPROPSET_SQLSERVERSESSION 속성 SSPROP_QUOTEDCATALOGNAMES가 VARIANT_TRUE이면 카탈로그 이름에 따옴표 붙은 식별자(예: "my.catalog")를 지정할 수 있습니다. Catalog에서 스키마 행 집합 출력을 제한할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 연결 된 서버 및 카탈로그 이름을 포함 하는 두 부분으로 구성 된 이름을 인식 합니다. 아래 표의 스키마 행 집합에 대해 두 부분으로 구성 된 카탈로그 이름을 _linked_server_로 지정 합니다 **.** _catalog_ 는 지정 된 연결 된 서버의 해당 카탈로그로 출력을 제한 합니다.  
  
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
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 연결 된 서버로 등록 된 OLE DB 데이터 원본 목록을 반환 하는 스키마 행 집합 LINKEDSERVERS를 정의 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스키마 행 집합 지원&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 행 &#40;집합 OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
