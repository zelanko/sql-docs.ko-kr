---
title: IRow::GetColumns 사용 | Microsoft Docs
description: IRow::GetColumns를 사용하여 행의 모든 열에 액세스
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
ms.openlocfilehash: 6f00e7c205e559864ed495dccd43f3a4f979260f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008771"
---
# <a name="using-irowgetcolumns"></a>IRow::GetColumns 사용
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **IRow** 구현에서는 열에 대한 정방향 전용 순차적 액세스를 허용합니다. **IRow::GetColumns**를 한 번 호출하거나 행의 여러 열에 액세스할 때마다 **IRow::GetColumns**를 여러 번 호출하여 행의 모든 열에 액세스할 수 있습니다.  
  
 **IRow::GetColumns**를 여러 번 호출할 때 겹치지 않도록 해야 합니다. 예를 들어 **IRow::GetColumns**에 대한 첫 번째 호출에서 열 1, 2, 3을 검색하는 경우 **IRow::GetColumns**에 대한 두 번째 호출은 열 4, 5, 6에 대한 호출이어야 합니다. 나중에 **IRow::GetColumns**에 대한 호출이 겹치면 상태 플래그(DBCOLUMNACCESS의 dwstatus 필드)가 DBSTATUS_E_UNAVAILABLE로 설정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [IRow를 사용하여 단일 행 페치](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
