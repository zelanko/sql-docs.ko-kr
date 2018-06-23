---
title: 트랜잭션을 | Microsoft Docs
description: SQL Server에 대 한 OLE DB 드라이버에서 트랜잭션
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 1f1e0b252960468e443b157c7c95213809a4d318
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689316"
---
# <a name="transactions"></a>의
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 로컬 트랜잭션 지원을 구현합니다. 소비자는 MS DTC(Microsoft Distributed Transaction Coordinator)를 사용하여 분산 또는 통합 트랜잭션을 사용할 수 있습니다. 여러 세션에 걸친 트랜잭션 제어가 필요한 소비자에는 OLE DB Driver for SQL Server 시작 하 고 MS DTC에서 유지 관리 하는 트랜잭션을 조인할 수 있습니다.  
  
 기본적으로는 OLE DB Driver for SQL Server 소비자 세션의 개별 동작이 각각의 인스턴스에 대해 전체 트랜잭션의 구성 하는 자동 커밋 트랜잭션 모드를 사용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. OLE DB 드라이버에서 SQL Server 자동 커밋 모드는 로컬 이며, 자동 커밋 트랜잭션이 벗어나지 단일 세션입니다.  
  
 OLE DB Driver for SQL Server 노출 된 **ITransactionLocal** 인터페이스를 명시적으로 사용 하 고 암시적으로의 인스턴스를 단일 연결에서 트랜잭션을 시작 소비자 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. OLE DB Driver for SQL Server에는 중첩 된 로컬 트랜잭션을 지원 하지 않습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [로컬 트랜잭션 지원](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [분산 트랜잭션 지원](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [격리 수준 &#40;OLE DB&#41;](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
