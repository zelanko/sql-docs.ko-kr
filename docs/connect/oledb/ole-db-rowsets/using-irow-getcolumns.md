---
title: 'Irow:: Getcolumns를 사용 하 여 | Microsoft Docs'
description: 'Irow:: Getcolumns를 사용 하 여 행의 모든 열에 액세스 하려면'
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: f210e06b3c1304251e52ad8fc3f3177fef5e5a10
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803772"
---
# <a name="using-irowgetcolumns"></a>IRow::GetColumns 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **IRow** 구현에서는 열에 대한 정방향 전용 순차적 액세스를 허용합니다. **IRow::GetColumns**를 한 번 호출하거나 행의 여러 열에 액세스할 때마다 **IRow::GetColumns**를 여러 번 호출하여 행의 모든 열에 액세스할 수 있습니다.  
  
 **IRow::GetColumns**를 여러 번 호출할 때 겹치지 않도록 해야 합니다. 예를 들어 **IRow::GetColumns**에 대한 첫 번째 호출에서 열 1, 2, 3을 검색하는 경우 **IRow::GetColumns**에 대한 두 번째 호출은 열 4, 5, 6에 대한 호출이어야 합니다. 나중에 **IRow::GetColumns**에 대한 호출이 겹치면 상태 플래그(DBCOLUMNACCESS의 dwstatus 필드)가 DBSTATUS_E_UNAVAILABLE로 설정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [IRow를 사용하여 단일 행 페치](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
