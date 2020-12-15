---
description: IDBProperties (Native Client OLE DB 공급자)
title: IDBProperties (Native Client OLE DB 공급자) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b053d4d1ec270fedc0a136d3aada29ed63a87071
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462184"
---
# <a name="idbproperties-native-client-ole-db-provider"></a>IDBProperties (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  OLE DB 표준 사양을 통해 공급자가 **DBPROPINFO::vValues** 에 대해 VT_EMPTY를 지정할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 **IDBProperties::GetPropertyInfo** 과 함께 호출하여 행 집합 속성을 검색하는 경우 **DBPROPSET_ROWSETALL** Native Client OLE DB에서 항상 VT_EMPTY를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스&#40;OLE DB&#41;](./sql-server-native-client-ole-db-interfaces.md)  
  
