---
description: 행 페치-다음 인출 (Native Client OLE DB 공급자)
title: 다음 인출 위치 (Native Client OLE DB 공급자) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0f1fd4da86bdd0c7cbe0df0c832554566e93b88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448393"
---
# <a name="fetching-rows---next-fetch--native-client-ole-db-provider"></a>행 페치-다음 인출 (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 다음 인출 위치를 추적 하 여 **GetNextRows** 메서드 (건너뛴 경우, 방향 변경 또는 **findnextrow**, **Seek**또는 **RestartPosition** 메서드에 대 한 중간 호출)에 대 한 호출 시퀀스에서 행을 건너뛰거나 반복 하지 않고 전체 행 집합을 읽습니다. **IRowset::GetNextRows**, **IRowset::RestartPosition** 또는 **IRowsetIndex::Seek**을 호출하거나 null *pBookmark* 값을 사용해 **FindNextRow**를 호출하여 다음 인출 위치를 변경할 수 있습니다. null이 아닌 *pBookmark* 값을 사용해 **FindNextRow**를 호출하면 다음 인출 위치가 변경되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 페치](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
  
