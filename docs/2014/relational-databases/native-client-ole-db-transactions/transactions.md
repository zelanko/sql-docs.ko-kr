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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dca9b7a3289390b1d1e20e1b0d18c23b44b87617
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63213898"
---
# <a name="transactions"></a>트랜잭션
  Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 로컬 트랜잭션 지원을 구현 합니다. 소비자는 MS DTC(Microsoft Distributed Transaction Coordinator)를 사용하여 분산 또는 통합 트랜잭션을 사용할 수 있습니다. 여러 세션에 걸친 트랜잭션 제어를 요구 하는 소비자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 경우 Native Client OLE DB 공급자는 MS DTC에서 시작 및 유지 관리 되는 트랜잭션을 조인할 수 있습니다.  
  
 기본적으로 Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 공급자는 자동 커밋 트랜잭션 모드를 사용 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 여기서 소비자 세션의 각 불연속 동작은 인스턴스에 대해 전체 트랜잭션을 구성 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 자동 커밋 모드는 로컬 이며 자동 커밋 트랜잭션은 단일 세션 이상으로 확장 되지 않습니다.  
  
 Native Client OLE DB 공급자는 소비자가 인스턴스에 대 한 단일 연결에서 명시적 및 암시적으로 트랜잭션을 사용할 수 있도록 **ITransactionLocal** 인터페이스를 노출 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 중첩 된 로컬 트랜잭션을 지원 하지 않습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [로컬 트랜잭션 지원](supporting-local-transactions.md)  
  
-   [분산 트랜잭션 지원](supporting-distributed-transactions.md)  
  
-   [격리 수준이 OLE DB &#40;&#41;](isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
