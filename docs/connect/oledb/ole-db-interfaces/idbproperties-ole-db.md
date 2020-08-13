---
title: IDBProperties(OLE DB 드라이버) | Microsoft Docs
description: IDBProperties 인터페이스(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: afaf7fc8e0ea60a1ee8576e0afa5b279653a2272
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244499"
---
# <a name="idbproperties-ole-db"></a>IDBProperties(OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB 표준 사양을 통해 공급자가 **DBPROPINFO::vValues**에 대해 VT_EMPTY를 지정할 수 있습니다. 그러나 **DBPROPSET_ROWSETALL**로 **IDBProperties::GetPropertyInfo**를 호출하여 행 집합 속성을 검색하는 경우 SQL Server용 OLE DB 드라이버에서 항상 VT_EMPTY를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
