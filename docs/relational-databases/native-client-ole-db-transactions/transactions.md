---
title: 트랜잭션을 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: 3b41e33a-c1ca-4b2a-9464-312b0ed3ca89
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: e80bd72fd6ec645637444add71264d29967cb81c
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39556443"
---
# <a name="transactions"></a>의
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 로컬 트랜잭션 지원을 구현 합니다. 소비자는 MS DTC(Microsoft Distributed Transaction Coordinator)를 사용하여 분산 또는 통합 트랜잭션을 사용할 수 있습니다. 여러 세션에 걸친 트랜잭션 제어가 필요한 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 트랜잭션을 시작 하 고 MS DTC에 의해 유지 관리를 조인할 수 있습니다.  
  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자 세션의 개별 동작이 각각의 인스턴스에 대해 전체 트랜잭션을 구성 하는 위치는 자동 커밋 트랜잭션 모드를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 자동 커밋 모드는 로컬 이며, 자동 커밋 트랜잭션이 단일 세션 둘 이상의 넘어가지 않습니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 하는 **ITransactionLocal** 인터페이스를 명시적으로 사용 하 여 암시적으로의 인스턴스를 단일 연결에서 트랜잭션을 시작 하는 소비자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 중첩 된 로컬 트랜잭션을 지원 하지 않습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [로컬 트랜잭션 지원](../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md)  
  
-   [분산 트랜잭션 지원](../../relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [격리 수준 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
