---
title: "Irow:: Getcolumns를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f4f66d36796de8c4dbb0c39b169314be9bdc473
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="using-irowgetcolumns"></a>IRow::GetColumns 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IRow** 구현 열에 정방향 전용 순차적 액세스를 허용 합니다. 한 번 호출 하는 행의 모든 열에 액세스 하거나 있습니다 **irow:: Getcolumns** 호출 또는 **irow:: Getcolumns** 여러 번 할 때마다 해당 행의 여러 열에 액세스 하는 것입니다.  
  
 에 여러 번 호출 **irow:: Getcolumns** 겹쳐서는 안 됩니다. 예를 들어, 첫 번째 호출을 **irow:: Getcolumns** 열 1, 2 및 3, 두 번째 호출을 검색 **irow:: Getcolumns** 열 4, 5 및 6에 대 한 호출 해야 합니다. 경우 나중에 대 한 호출이 **irow:: Getcolumns** 겹치면 상태 플래그 (DBCOLUMNACCESS의 dwstatus 필드) DBSTATUS_E_UNAVAILABLE로 설정 되어 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [IRow를 사용하여 단일 행 페치](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
