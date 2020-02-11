---
title: 상속 된 트랜잭션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], inherited
- child packages
- inherited transactions [Integration Services]
ms.assetid: 90db5564-d41e-4cfe-8c9e-4e68d41eff1c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d8e22375e660e6bcd55c8075edaaba067160279d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058060"
---
# <a name="inherited-transactions"></a>상속된 트랜잭션
  패키지 실행 태스크를 사용하면 패키지가 다른 패키지를 실행할 수 있습니다. 패키지 실행 태스크에서 실행하는 패키지인 자식 패키지는 자체의 패키지 트랜잭션을 만들거나 부모 패키지 트랜잭션을 상속할 수 있습니다.  
  
 다음 두 가지 조건에 모두 해당하면 자식 패키지는 부모 패키지 트랜잭션을 상속합니다.  
  
-   패키지 실행 태스크가 패키지를 호출합니다.  
  
-   패키지를 호출한 패키지 실행 태스크가 부모 패키지 트랜잭션도 조인했습니다.  
  
 자식 패키지가 트랜잭션에 조인하지 않으면 자식 패키지 내의 컨테이너 및 태스크가 부모 패키지 트랜잭션에 조인할 수 없습니다.  
  
## <a name="illustration-of-package-transactions"></a>패키지 트랜잭션의 그림  
 다음 다이어그램에서 트랜잭션을 사용하는 3개의 패키지가 있습니다. 각 패키지는 여러 태스크를 포함합니다. 트랜잭션 동작을 강조하기 위해 패키지 실행 태스크만 표시했습니다. 패키지 A는 패키지 B와 C를 실행하고 차례로 패키지 B는 패키지 D와 E를 실행하며 패키지 C는 패키지 F를 실행합니다.  
  
 패키지 및 태스크는 다음 트랜잭션 특성을 가집니다.  
  
-   **TransactionOption** 은 패키지 A와 C에서 **필수** 로 설정 됩니다.  
  
-   **TransactionOption** 은 패키지 b 및 d에서 지원 되는로 설정 되 고, 패키지 실행 b, 패키지 실행 D 및 패키지 실행 F에서 **지원** 됩니다.  
  
-   **TransactionOption** 는 패키지 E, 패키지 실행 C 및 패키지 실행 E에서 **notsupported** 로 설정 됩니다.  
  
 ![상속된 트랜잭션의 흐름](media/mw-dts-executepack.gif "상속된 트랜잭션의 흐름")  
  
 패키지 B, D 및 F만 부모 패키지에서 트랜잭션을 상속할 수 있습니다.  
  
 패키지 B 및 D는 패키지 A가 시작한 트랜잭션을 상속합니다.  
  
 패키지 F는 패키지 C가 시작한 트랜잭션을 상속합니다.  
  
 패키지 A와 C는 자체 트랜잭션을 제어합니다.  
  
 패키지 E는 트랜잭션을 사용하지 않습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [트랜잭션을 사용하도록 패키지 구성](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
