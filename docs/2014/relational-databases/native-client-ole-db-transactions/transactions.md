---
title: 트랜잭션 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: 3b41e33a-c1ca-4b2a-9464-312b0ed3ca89
author: rothja
ms.author: jroth
ms.openlocfilehash: 1067820e80f9c7a4e1af2c8a14c85bc9dbfdd6aa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85017608"
---
# <a name="transactions"></a>트랜잭션
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 로컬 트랜잭션 지원을 구현 합니다. 소비자는 MS DTC(Microsoft Distributed Transaction Coordinator)를 사용하여 분산 또는 통합 트랜잭션을 사용할 수 있습니다. 여러 세션에 걸친 트랜잭션 제어를 요구 하는 소비자의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 MS DTC에서 시작 및 유지 관리 되는 트랜잭션을 조인할 수 있습니다.  
  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 자동 커밋 트랜잭션 모드를 사용 합니다. 여기서 소비자 세션의 각 불연속 동작은 인스턴스에 대해 전체 트랜잭션을 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 자동 커밋 모드는 로컬 이며 자동 커밋 트랜잭션은 단일 세션 이상으로 확장 되지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 소비자가 인스턴스에 대 한 단일 연결에서 명시적 및 암시적으로 트랜잭션을 사용할 수 있도록 **ITransactionLocal** 인터페이스를 노출 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 중첩 된 로컬 트랜잭션을 지원 하지 않습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [로컬 트랜잭션 지원](supporting-local-transactions.md)  
  
-   [분산 트랜잭션 지원](supporting-distributed-transactions.md)  
  
-   [격리 수준&#40;OLE DB&#41;](isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
