---
title: 트랜잭션 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버의 트랜잭션
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 64a05f57c40027a4db448a987d32f77d62f0a837
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011231"
---
# <a name="transactions"></a>트랜잭션
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 로컬 트랜잭션 지원을 구현합니다. 소비자는 MS DTC(Microsoft Distributed Transaction Coordinator)를 사용하여 분산 또는 통합 트랜잭션을 사용할 수 있습니다. 여러 세션에 걸친 트랜잭션 제어가 필요한 소비자를 위해 SQL Server용 OLE DB 드라이버는 MS DTC에서 시작 및 유지 관리되는 트랜잭션을 조인할 수 있습니다.  
  
 기본적으로 SQL Server용 OLE DB 드라이버는 자동 커밋 트랜잭션 모드를 사용하며, 이 경우 소비자 세션의 개별 동작이 각각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 전체 트랜잭션을 구성합니다. SQL Server용 OLE DB 드라이버 자동 커밋 모드는 로컬이며, 자동 커밋 트랜잭션이 단일 세션을 벗어나지 않습니다.  
  
 SQL Server용 OLE DB 드라이버는 **ITransactionLocal** 인터페이스를 노출하여 소비자가 명시적 및 암시적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 단일 연결에서 시작 트랜잭션을 사용할 수 있게 합니다. OLE DB Driver for SQL Server는 중첩된 로컬 트랜잭션을 지원하지 않습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [로컬 트랜잭션 지원](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [분산 트랜잭션 지원](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [격리 수준&#40;OLE DB&#41;](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
