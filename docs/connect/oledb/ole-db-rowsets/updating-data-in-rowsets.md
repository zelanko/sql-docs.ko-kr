---
title: 행 집합의 데이터 업데이트(OLE DB 드라이버)
description: 소비자가 SQL Server 데이터가 포함된 수정할 수 있는 행 집합을 업데이트하면 OLE DB Driver for SQL Server가 해당 데이터를 업데이트하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, updating data
- OLE DB Driver for SQL Server, data updates
- data updates [SQL Server], OLE DB
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 40bb8663cd2d49ceaeda2305797fb42bdacc4324
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859958"
---
# <a name="updating-data-in-rowsets"></a>행 집합의 데이터 업데이트
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  소비자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터가 포함된 수정할 수 있는 행 집합을 업데이트하면 OLE DB Driver for SQL Server가 해당 데이터를 업데이트합니다. 수정할 수 있는 행 집합은 소비자가 **IRowsetChange** 또는 **IRowsetUpdate** 인터페이스에 대한 지원을 요청할 때 생성됩니다.  
  
 OLE DB Driver for SQL Server가 수정할 수 있는 행 집합은 모두 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서를 사용하여 행 집합을 지원합니다. 행 집합 속성 DBPROP_LOCKMODE는 커서의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 동시성 제어 동작을 변경하고 업데이트할 수 있는 행 집합의 데이터 무결성 오류 생성과 행 집합 행 인출 동작을 결정합니다.  
  
 OLE DB Driver for SQL Server는 업데이트 전후로 행 동기화를 지원합니다.  
  
> [!NOTE]  
>  IRowChange::SetColumns를 사용하여 행 개체에 대한 하나 이상의 명명된 열 값을 설정할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQL Server 커서의 데이터 업데이트](../../oledb/ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [행 다시 동기화](../../oledb/ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>참고 항목  
 [행 집합](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
