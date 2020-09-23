---
title: 다음 페치 위치(OLE DB 드라이버) | Microsoft Docs
description: OLE DB Driver for SQL Server는 GetNextRows 메서드에 대한 호출 시퀀스에서 전체 행 집합을 읽도록 다음 페치 위치를 계속 추적합니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ba713e9da40255d992e7cccf8c8430a205cadf4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861587"
---
# <a name="fetching-rows---next-fetch-position-ole-db-driver"></a>행 페치 - 다음 페치 위치(OLE DB 드라이버)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server용 OLE DB 드라이버는 **GetNextRows** 메서드 호출 시퀀스에서 어떤 행도 건너뛰거나 반복하지 않고(행을 건너뛰거나 방향을 변경하거나 중간에 **FindNextRow**, **Seek** 또는 **RestartPosition** 메서드를 호출하지 않음) 전체 행 집합을 읽을 수 있도록 다음 인출 위치를 추적합니다. **IRowset::GetNextRows**, **IRowset::RestartPosition** 또는 **IRowsetIndex::Seek**을 호출하거나 null *pBookmark* 값을 사용해 **FindNextRow**를 호출하여 다음 인출 위치를 변경할 수 있습니다. null이 아닌 *pBookmark* 값을 사용해 **FindNextRow**를 호출하면 다음 인출 위치가 변경되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 페치](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
