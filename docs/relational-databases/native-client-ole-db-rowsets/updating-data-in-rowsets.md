---
title: 행 집합의 데이터 업데이트 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, updating data
- SQL Server Native Client OLE DB provider, data updates
- data updates [SQL Server], OLE DB
ms.assetid: 37769b1c-c480-419a-8c54-5cc420bf73db
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d70cbc3743b1ba0ded077b810c0af7a4af81cab
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="updating-data-in-rowsets"></a>행 집합의 데이터 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 업데이트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 소비자는 해당 데이터를 포함 하는 수정 가능한 행 집합을 업데이트 한 경우. 수정 가능한 행 집합을 소비자 하나에 대 한 지원을 요청할 때 만들어집니다는 **IRowsetChange** 또는 **IRowsetUpdate** 인터페이스입니다.  
  
 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 수정할 수 있는 행 집합에 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서를 행 집합을 지원 합니다. 행 집합 속성 DBPROP_LOCKMODE는 커서의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동시성 제어 동작을 변경하고 업데이트할 수 있는 행 집합의 데이터 무결성 오류 생성과 행 집합 행 인출 동작을 결정합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 행 동기화 하기 전이나 후 업데이트를 지원 합니다.  
  
> [!NOTE]  
>  IRowChange::SetColumns를 사용하여 행 개체에 대한 하나 이상의 명명된 열 값을 설정할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQL Server 커서의 데이터 업데이트](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [행 다시 동기화](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>관련 항목:  
 [행 집합](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
