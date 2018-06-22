---
title: IDBProperties (OLE DB) | Microsoft Docs
description: IDBProperties 인터페이스 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d2b5fa37e7cacb6ae29a260ceb6e57089b85e817
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689826"
---
# <a name="idbproperties-ole-db"></a>IDBProperties(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB 표준 사양을 통해 공급자가 **DBPROPINFO::vValues**에 대해 VT_EMPTY를 지정할 수 있습니다. 그러나 OLE DB Driver for SQL Server OLE DB 항상 VT_EMPTY를 반환를 호출할 때 **idbproperties:: Getpropertyinfo** 와 **DBPROPSET_ROWSETALL** 행 집합 속성을 검색 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [인터페이스 &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
