---
title: 다음 인출 위치 | Microsoft Docs
description: 가져오는 행-다음 인출 위치
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
ms.openlocfilehash: 46e6e3b9898d6c1adbe4df4bdc2b33444b623df9
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690116"
---
# <a name="fetching-rows---next-fetch-position"></a>가져오는 행-다음 인출 위치
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver 유지 하는 SQL Server에 대 한 트랙에 다음 인출 위치 하므로 하는 호출의 시퀀스는 **GetNextRows** 메서드 (없이 건너뛰고, 방향, 또는 중간 변경 내용에 대 한 호출이 **FindNextRow** **Seek**, 또는 **restartposition이** 메서드) 건너뛰는 중 또는 모든 행을 반복 하지 않고 전체 행 집합을 읽습니다. 다음 인출 위치를 변경할 호출 하 여 **irowset:: Getnextrows**, **irowset:: Restartposition**, 또는 **IRowsetIndex::Seek**, 를호출하여**FindNextRow** null *pBookmark* 값입니다. 호출 **FindNextRow** null이 아닌와 *pBookmark* 값은 다음 인출 위치에 영향을 주지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [행 페치](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
