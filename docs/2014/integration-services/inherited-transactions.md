---
title: 트랜잭션을 상속 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactions [Integration Services], inherited
- child packages
- inherited transactions [Integration Services]
ms.assetid: 90db5564-d41e-4cfe-8c9e-4e68d41eff1c
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0df0ba113b23e9b5cc582b1795299a0befee4bae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180932"
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
  
-   패키지 A 및 C의**트랜잭션 옵션** 은 **필수** 로 설정됩니다.  
  
-   패키지 B 및 D, 패키지 실행 태스크 B, 패키지 실행 D 및 패키지 실행 F의**트랜잭션 옵션** 은 **지원** 으로 설정됩니다.  
  
-   패키지 E, 패키지 실행 태스크 C 및 패키지 실행 E의**트랜잭션 옵션** 은 **지원되지 않음** 으로 설정됩니다.  
  
 ![상속된 트랜잭션의 흐름](media/mw-dts-executepack.gif "상속된 트랜잭션의 흐름")  
  
 패키지 B, D 및 F만 부모 패키지에서 트랜잭션을 상속할 수 있습니다.  
  
 패키지 B 및 D는 패키지 A가 시작한 트랜잭션을 상속합니다.  
  
 패키지 F는 패키지 C가 시작한 트랜잭션을 상속합니다.  
  
 패키지 A와 C는 자체 트랜잭션을 제어합니다.  
  
 패키지 E는 트랜잭션을 사용하지 않습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [트랜잭션을 사용하도록 패키지 구성](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  