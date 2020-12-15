---
description: SQL Server Native Client의 트랜잭션
title: 트랜잭션 (Native Client OLE DB 공급자)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: 3b41e33a-c1ca-4b2a-9464-312b0ed3ca89
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2ed64680091b7b1170de641c9e1fe04d825dc044
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462114"
---
# <a name="transactions-in-sql-server-native-client"></a>SQL Server Native Client의 트랜잭션
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 로컬 트랜잭션 지원을 구현 합니다. 소비자는 MS DTC(Microsoft Distributed Transaction Coordinator)를 사용하여 분산 또는 통합 트랜잭션을 사용할 수 있습니다. 여러 세션에 걸친 트랜잭션 제어를 요구 하는 소비자의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 MS DTC에서 시작 및 유지 관리 되는 트랜잭션을 조인할 수 있습니다.  
  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 자동 커밋 트랜잭션 모드를 사용 합니다. 여기서 소비자 세션의 각 불연속 동작은 인스턴스에 대해 전체 트랜잭션을 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 자동 커밋 모드는 로컬 이며 자동 커밋 트랜잭션은 단일 세션 이상으로 확장 되지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 소비자가 인스턴스에 대 한 단일 연결에서 명시적 및 암시적으로 트랜잭션을 사용할 수 있도록 **ITransactionLocal** 인터페이스를 노출 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 중첩 된 로컬 트랜잭션을 지원 하지 않습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [로컬 트랜잭션 지원](../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md)  
  
-   [분산 트랜잭션 지원](../../relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [격리 수준&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
