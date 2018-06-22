---
title: 행 집합의 데이터 업데이트 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 행 집합의 데이터 업데이트
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
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, updating data
- OLE DB Driver for SQL Server, data updates
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 009c6023dc1905ac724287790c1b26a4bfcf87d3
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689906"
---
# <a name="updating-data-in-rowsets"></a>행 집합의 데이터 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB 드라이버에서 SQL Server 업데이트 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 소비자는 해당 데이터를 포함 하는 수정 가능한 행 집합을 업데이트 한 경우. 수정 가능한 행 집합을 소비자 하나에 대 한 지원을 요청할 때 만들어집니다는 **IRowsetChange** 또는 **IRowsetUpdate** 인터페이스입니다.  
  
 모든 OLE DB Driver for SQL Server가 수정할 수 있는 행 집합 사용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서를 행 집합을 지원 합니다. 행 집합 속성 DBPROP_LOCKMODE는 커서의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 동시성 제어 동작을 변경하고 업데이트할 수 있는 행 집합의 데이터 무결성 오류 생성과 행 집합 행 인출 동작을 결정합니다.  
  
 OLE DB Driver for SQL Server 업데이트 하기 전후에 행 동기화를 지원합니다.  
  
> [!NOTE]  
>  IRowChange::SetColumns를 사용하여 행 개체에 대한 하나 이상의 명명된 열 값을 설정할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQL Server 커서의 데이터 업데이트](../../oledb/ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [행 다시 동기화](../../oledb/ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>관련 항목  
 [행 집합](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
