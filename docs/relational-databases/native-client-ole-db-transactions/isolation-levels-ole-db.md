---
title: 격리 수준 (Native Client OLE DB 공급자) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d828877a5b1f685eb5e00c5649acd50fd925aabc
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87240233"
---
# <a name="isolation-levels-native-client-ole-db-provider"></a>격리 수준 (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트는 연결에 대한 트랜잭션 격리 수준을 제어할 수 있습니다. Native Client OLE DB 공급자 소비자는 트랜잭션 격리 수준을 제어 하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음을 사용 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 기본 자동 커밋 모드의 DBPROPSET_SESSION 속성 DBPROP_SESS_AUTOCOMMITISOLEVELS입니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]수준에 대 한 Native Client OLE DB 공급자 기본값은 DBPROPVAL_TI_READCOMMITTED입니다.  
  
-   로컬 수동 커밋 트랜잭션에 대한 **ITransactionLocal::StartTransaction** 메서드의 *isoLevel* 매개 변수를 사용합니다.  
  
-   MS DTC 통합 분산 트랜잭션에 대해 **ITransactionDispenser::BeginTransaction** 메서드의 *isoLevel* 매개 변수를 사용합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하면 커밋되지 않은 읽기 격리 수준에서 읽기 전용으로 액세스할 수 있습니다. 이외의 다른 모든 수준은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체에 잠금을 적용하므로 동시성을 제한합니다. 클라이언트에 더 높은 동시성 수준이 필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 데이터 동시 액세스에 대해 더 높은 수준의 제한을 적용합니다. 데이터에 대 한 동시 액세스의 최고 수준을 유지 하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자는 특정 동시성 수준에 대 한 요청을 지능적으로 제어 해야 합니다.  
  
> [!NOTE]  
>  스냅샷 격리 수준은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입되었습니다. 자세한 내용은 [Working with Snapshot Isolation](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
