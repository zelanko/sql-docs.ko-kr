---
title: 스키마 행 집합에서 분산 쿼리 지원 | Microsoft Docs
description: 스키마 행 집합에서 분산 쿼리 지원
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], OLE DB Driver for SQL Server
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa604a66d953a4e25c3df3f20fb32218e179451b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="schema-rowsets---distributed-query-support"></a>스키마 행 집합-분산된 쿼리 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  지원 하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 분산 쿼리에서 OLE DB Driver for SQL Server **IDBSchemaRowset** 인터페이스가 연결 된 서버에서 메타 데이터를 반환 합니다.  
  
 DBPROPSET_SQLSERVERSESSION 속성 SSPROP_QUOTEDCATALOGNAMES가 VARIANT_TRUE이면 카탈로그 이름에 따옴표 붙은 식별자(예: "my.catalog")를 지정할 수 있습니다. 카탈로그에서 스키마 행 집합 출력을 제한 하는 경우는 OLE DB Driver for SQL Server 연결 된 서버 이름과 카탈로그를 포함 하는 두 부분으로 이루어진 이름을 인식 합니다. 지정 하는 두 부분으로 구성 된 카탈로그 이름을 아래 표의 스키마 행 집합에 대 한 *linked_server ***.*** 카탈로그* 명명 된 연결 된 서버에 적용 가능한 카탈로그로 출력이 제한 합니다.  
  
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
>  모든 카탈로그에 연결된 된 서버에서 스키마 행 집합을 제한 하는 구문을 사용 하 여 *linked_server* (여기서 마침표 구분 기호는 이름 사양에 포함). 이 구문은 카탈로그 이름 제한에 NULL을 지정하는 것과 같으며 연결된 서버가 카탈로그를 지원하지 않는 데이터 원본을 나타내는 경우에도 사용됩니다.  
  
 OLE DB Driver for SQL Server 정의 스키마 행 집합 LINKEDSERVERS를 연결 된 서버로 등록 된 OLE DB 데이터 원본 목록을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스키마 행 집합 지원 &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 행 집합 &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
