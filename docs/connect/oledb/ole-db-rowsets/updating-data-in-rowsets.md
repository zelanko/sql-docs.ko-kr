---
title: 행 집합의 데이터를 업데이트 하는 중 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하는 행 집합의 데이터를 업데이트 하는 중
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
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 3e6a03d5bc379b620db06e0f1308058d647397e1
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803777"
---
# <a name="updating-data-in-rowsets"></a>행 집합의 데이터 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  소비자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터가 포함된 수정할 수 있는 행 집합을 업데이트하면 OLE DB Driver for SQL Server가 해당 데이터를 업데이트합니다. 수정할 수 있는 행 집합은 소비자가 **IRowsetChange** 또는 **IRowsetUpdate** 인터페이스에 대한 지원을 요청할 때 생성됩니다.  
  
 모든 OLE DB Driver for SQL Server가 수정할 수 있는 행 집합 사용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서를 행 집합을 지원 합니다. 행 집합 속성 DBPROP_LOCKMODE는 커서의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 동시성 제어 동작을 변경하고 업데이트할 수 있는 행 집합의 데이터 무결성 오류 생성과 행 집합 행 인출 동작을 결정합니다.  
  
 OLE DB Driver for SQL Server를 업데이트 하기 전후에 행 동기화를 지원합니다.  
  
> [!NOTE]  
>  IRowChange::SetColumns를 사용하여 행 개체에 대한 하나 이상의 명명된 열 값을 설정할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQL Server 커서의 데이터 업데이트](../../oledb/ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [행 다시 동기화](../../oledb/ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>참고 항목  
 [행 집합](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
