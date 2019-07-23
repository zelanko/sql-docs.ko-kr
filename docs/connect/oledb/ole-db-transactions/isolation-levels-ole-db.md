---
title: 격리 수준 (OLE DB) | Microsoft Docs
description: 격리 수준(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2c9f3a7cd06f801555ab373e7e54fbf1b620d894
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993966"
---
# <a name="isolation-levels-ole-db"></a>격리 수준(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트는 연결에 대한 트랜잭션 격리 수준을 제어할 수 있습니다. 트랜잭션 격리 수준을 제어 하기 위해 SQL Server 소비자 용 OLE DB 드라이버는 다음을 사용 합니다.  
  
-   SQL Server용 OLE DB 드라이버 기본 자동 커밋 모드에 대해 DBPROPSET_SESSION 속성 DBPROP_SESS_AUTOCOMMITISOLEVELS를 사용합니다.  
  
     수준에 대 한 OLE DB 드라이버 SQL Server 기본값은 DBPROPVAL_TI_READCOMMITTED입니다.  
  
-   로컬 수동 커밋 트랜잭션에 대한 **ITransactionLocal::StartTransaction** 메서드의 *isoLevel* 매개 변수를 사용합니다.  
  
-   MS DTC 통합 분산 트랜잭션에 대해 **ITransactionDispenser::BeginTransaction** 메서드의 *isoLevel* 매개 변수를 사용합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용하면 커밋되지 않은 읽기 격리 수준에서 읽기 전용으로 액세스할 수 있습니다. 이외의 다른 모든 수준은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체에 잠금을 적용하므로 동시성을 제한합니다. 클라이언트에 더 높은 동시성 수준이 필요한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 데이터 동시 액세스에 대해 더 높은 수준의 제한을 적용합니다. 최고 수준의 데이터 동시 액세스를 유지하려면 SQL Server용 OLE DB 드라이버 소비자가 특정 동시성 수준에 대한 요청을 지능적으로 제어해야 합니다.  
  
> [!NOTE]  
>  스냅샷 격리 수준은 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 도입되었습니다. 자세한 내용은 [Working with Snapshot Isolation](../../oledb/features/working-with-snapshot-isolation.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션](../../oledb/ole-db-transactions/transactions.md)  
  
  
