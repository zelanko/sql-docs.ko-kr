---
title: 'Irow:: Getcolumns를 사용 하 여 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 8979f747a811bb67fbff54acb16627469077063f
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39536933"
---
# <a name="using-irowgetcolumns"></a>IRow::GetColumns 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IRow** 구현에서는 열에 대한 정방향 전용 순차적 액세스를 허용합니다. **IRow::GetColumns**를 한 번 호출하거나 행의 여러 열에 액세스할 때마다 **IRow::GetColumns**를 여러 번 호출하여 행의 모든 열에 액세스할 수 있습니다.  
  
 **IRow::GetColumns**를 여러 번 호출할 때 겹치지 않도록 해야 합니다. 예를 들어 **IRow::GetColumns**에 대한 첫 번째 호출에서 열 1, 2, 3을 검색하는 경우 **IRow::GetColumns**에 대한 두 번째 호출은 열 4, 5, 6에 대한 호출이어야 합니다. 나중에 **IRow::GetColumns**에 대한 호출이 겹치면 상태 플래그(DBCOLUMNACCESS의 dwstatus 필드)가 DBSTATUS_E_UNAVAILABLE로 설정됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [IRow를 사용하여 단일 행 페치](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
