---
title: 스키마 행 집합에서 분산 쿼리 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7f7c5746a34ca40d567886cce6bce4b9b8aceb76
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181331"
---
# <a name="distributed-query-support-in-schema-rowsets"></a>스키마 행 집합에서 분산 쿼리 지원
  지원 하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 분산 쿼리에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 **IDBSchemaRowset** 인터페이스가 연결 된 서버에서 메타 데이터를 반환 합니다.  
  
 DBPROPSET_SQLSERVERSESSION 속성 SSPROP_QUOTEDCATALOGNAMES가 VARIANT_TRUE이면 카탈로그 이름에 따옴표 붙은 식별자(예: "my.catalog")를 지정할 수 있습니다. 스키마 행 집합 출력을 카탈로그 별로 제한 하면는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 연결 된 서버 및 카탈로그 이름을 포함 하는 두 부분으로 이루어진 이름을 인식 합니다. 지정 하는 두 부분으로 구성 된 카탈로그 이름을 아래 표의 스키마 행 집합에 대 한 *linked_server ***.*** 카탈로그* 명명 된 연결 된 서버에 적용 가능한 카탈로그로 출력이 제한 합니다.  
  
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
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 정의 스키마 행 집합 LINKEDSERVERS를 연결 된 서버로 등록 된 OLE DB 데이터 원본 목록을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [스키마 행 집합 지원 &#40;OLE DB&#41;](schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 행 집합 &#40;OLE DB&#41;](schema-rowsets-linkedservers-rowset.md)  
  
  