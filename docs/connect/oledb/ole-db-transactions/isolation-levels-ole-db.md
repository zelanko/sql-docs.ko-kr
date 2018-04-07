---
title: 격리 수준 (OLE DB) | Microsoft Docs
description: 격리 수준(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f40f3936fbf4ace09ff1df6a18ef86bc00747fd4
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="isolation-levels-ole-db"></a>격리 수준(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트는 연결에 대한 트랜잭션 격리 수준을 제어할 수 있습니다. 트랜잭션 격리 수준을 제어 하려면 OLE DB 드라이버에서 SQL Server 소비자를 사용 합니다.  
  
-   DBPROPSET_SESSION 속성 DBPROP_SESS_AUTOCOMMITISOLEVELS는 OLE DB Driver for SQL Server 기본 자동 커밋 모드에 대 한입니다.  
  
     OLE DB 드라이버는 수준에 대 한 SQL Server 기본값은 DBPROPVAL_TI_READCOMMITTED입니다.  
  
-   *isoLevel* 의 매개 변수는 **itransactionlocal:: Starttransaction** 로컬 수동 커밋 트랜잭션에 대 한 메서드.  
  
-   *isoLevel* 의 매개 변수는 **itransactiondispenser:: Begintransaction** 방법을 MS DTC 통합 분산 트랜잭션을 합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용하면 커밋되지 않은 읽기 격리 수준에서 읽기 전용으로 액세스할 수 있습니다. 이외의 다른 모든 수준은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체에 잠금을 적용하므로 동시성을 제한합니다. 클라이언트에 더 높은 동시성 수준이 필요한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 데이터 동시 액세스에 대해 더 높은 수준의 제한을 적용합니다. 가장 높은 수준의 데이터에 대 한 동시 액세스를 유지 하려면 OLE DB 드라이버에서 SQL Server 소비자의 요청을 특정 동시성 수준에 대 한를 지능적으로 제어 해야 합니다.  
  
> [!NOTE]  
>  스냅숏 격리 수준은 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 도입되었습니다. 자세한 내용은 참조 [스냅숏 격리 작업](../../oledb/features/working-with-snapshot-isolation.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [트랜잭션](../../oledb/ole-db-transactions/transactions.md)  
  
  
