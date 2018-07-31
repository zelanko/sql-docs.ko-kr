---
title: 다음 인출 위치 | Microsoft Docs
description: 행 인출 - 다음 인출 위치
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ec1149b615c64f2113afc007c0ea04e4c4665698
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39106109"
---
# <a name="fetching-rows---next-fetch-position"></a>행 인출 - 다음 인출 위치
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server용 OLE DB 드라이버는 **GetNextRows** 메서드 호출 시퀀스에서 어떤 행도 건너뛰거나 반복하지 않고(행을 건너뛰거나 방향을 변경하거나 중간에 **FindNextRow**, **Seek** 또는 **RestartPosition** 메서드를 호출하지 않음) 전체 행 집합을 읽을 수 있도록 다음 인출 위치를 추적합니다. **IRowset::GetNextRows**, **IRowset::RestartPosition** 또는 **IRowsetIndex::Seek**을 호출하거나 null *pBookmark* 값을 사용해 **FindNextRow**를 호출하여 다음 인출 위치를 변경할 수 있습니다. null이 아닌 *pBookmark* 값을 사용해 **FindNextRow**를 호출하면 다음 인출 위치가 변경되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 페치](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
