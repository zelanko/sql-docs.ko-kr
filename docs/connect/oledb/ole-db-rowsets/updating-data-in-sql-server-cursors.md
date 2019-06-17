---
title: SQL Server 커서의 데이터를 업데이트 하는 중 | Microsoft Docs
description: SQL Server 커서의 데이터 업데이트
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 5cb6c20746746d3261593e13978be022af8938a6
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803822"
---
# <a name="updating-data-in-sql-server-cursors"></a>SQL Server 커서의 데이터 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서를 통해 데이터를 인출하고 업데이트할 때는 SQL Server용 OLE DB 드라이버 소비자 애플리케이션에 다른 모든 클라이언트 애플리케이션에 적용되는 것과 동일한 고려 사항 및 제약 조건이 적용됩니다.  
  
 동시 데이터 액세스 제어에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서의 행만 참여합니다. 소비자가 수정이 가능한 행 집합을 요청하면 DBPROP_LOCKMODE에서 동시성 제어를 관리합니다. 소비자는 행 집합을 열기 전에 DBPROP_LOCKMODE 속성을 설정하여 동시 액세스 제어의 수준을 변경합니다.  
  
 트랜잭션이 오랫동안 열려 있을 수 있도록 설계된 클라이언트 응용 프로그램의 경우 트랜잭션 격리 수준 때문에 행 위치 지정에 상당한 시간 지연이 발생할 수 있습니다. 기본적으로 SQL Server용 OLE DB 드라이버는 DBPROPVAL_TI_READCOMMITTED로 지정되는 커밋된 읽기 격리 수준을 사용합니다. OLE DB Driver for SQL Server 행 집합 동시성이 읽기 전용일 때 더티 읽기 격리를 지원 합니다. 따라서 소비자는 수정이 가능한 행 집합에 더 높은 수준의 격리를 요청할 수 있지만 더 낮은 수준은 요청할 수 없습니다.  
  
## <a name="immediate-and-delayed-update-modes"></a>즉시 및 지연 업데이트 모드  
 즉시 업데이트 모드에서는 **IRowsetChange::SetData**를 호출할 때마다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 왕복이 발생합니다. 소비자가 단일 행을 여러 번 변경한 경우 **SetData**를 한 번 호출하여 모든 변경 내용을 전송하는 것이 효율적입니다.  
  
 지연 업데이트 모드에서는 **IRowsetUpdate::Update**의 *cRows* 및 *rghRows* 매개 변수에 지정된 각 행에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로의 왕복이 수행됩니다.  
  
 두 모드 모두 왕복은 행 집합에 대해 열려 있는 트랜잭션 개체가 없는 경우 고유한 트랜잭션을 나타냅니다.  
  
 사용 하는 경우 **irowsetupdate:: Update**에 OLE DB Driver for SQL Server가 지정 된 각 행을 처리 하려고 합니다. 행에서 잘못된 데이터, 길이 또는 상태 값 때문에 오류가 발생하더라도 SQL Server용 OLE DB 드라이버는 처리를 중지하지 않습니다. 업데이트에 참여하는 행은 모두 수정되거나 전혀 수정되지 않습니다. SQL Server용 OLE DB 드라이버가 DB_S_ERRORSOCCURRED를 반환하면 소비자는 반환된 *prgRowStatus* 배열을 조사하여 문제가 발생한 행이 있는지 확인해야 합니다.  
  
 소비자는 행이 특정한 순서로 처리된다고 가정해서는 안 됩니다. 소비자가 두 개 이상의 행에서 수정된 데이터를 순서대로 처리해야 하는 경우에는 응용 프로그램 논리에서 이러한 순서를 설정하고 트랜잭션을 열어 여기에 프로세스를 넣어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 집합의 데이터 업데이트](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
