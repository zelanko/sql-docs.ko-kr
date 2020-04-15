---
title: 트랜잭션 | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8779b68d6ab1070514f8ef6685ef378437d09539
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302540"
---
# <a name="transactions"></a>트랜잭션
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 로컬 트랜잭션 지원을 구현합니다. 소비자는 MS DTC(Microsoft Distributed Transaction Coordinator)를 사용하여 분산 또는 통합 트랜잭션을 사용할 수 있습니다. 여러 세션에 걸쳐 트랜잭션 제어가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 필요한 소비자의 경우 네이티브 클라이언트 OLE DB 공급자는 MS DTC에서 시작하고 유지 관리하는 트랜잭션에 참여할 수 있습니다.  
  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 자동 커밋 트랜잭션 모드를 사용하며, 여기서 소비자 세션의 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]불연속 작업은 의 인스턴스에 대한 전체 트랜잭션으로 구성됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 자동 커밋 모드는 로컬이며 자동 커밋 트랜잭션은 단일 세션이상에 걸쳐 없습니다.  
  
 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 **ITransactionLocal** 인터페이스를 노출하여 소비자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 대한 단일 연결에서 명시적으로 암시적으로 트랜잭션을 시작할 수 있도록 합니다. 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 중첩된 로컬 트랜잭션을 지원하지 않습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [로컬 트랜잭션 지원](../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md)  
  
-   [분산 트랜잭션 지원](../../relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [격리 수준&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
