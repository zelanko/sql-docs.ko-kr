---
title: 고유하게 컴파일된 저장 프로시저를 호출하는 최선의 구현 방법 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1dbc3dd467aab0cf60cdb255165767fc12a0f518
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63156775"
---
# <a name="best-practices-for-calling-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저를 호출하는 최선의 구현 방법
  고유하게 컴파일된 저장 프로시저의 특징  
  
-   애플리케이션에서 성능이 중요한 부분에 주로 사용됩니다.  
  
-   자주 실행됩니다.  
  
-   매우 빠를 것으로 예상됩니다.  
  
 고유하게 컴파일된 저장 프로시저를 사용하는 경우의 성능 이점은 행 수와 프로시저에서 처리하는 논리의 양이 많을수록 커집니다. 예를 들어 고유하게 컴파일된 저장 프로시저는 다음 중 하나 이상을 사용하는 경우 성능이 향상됩니다.  
  
-   집계.  
  
-   중첩 루프 조인  
  
-   다중 문 선택, 삽입, 업데이트 및 삭제 작업  
  
-   복잡한 식  
  
-   조건문, 루프 등의 절차적 논리  
  
 단일 행만 처리해야 하는 경우 고유하게 컴파일된 저장 프로시저를 사용하면 성능 이점이 제공되지 않을 수 있습니다.  
  
 서버에서 매개 변수 이름을 매핑하고 형식을 변환하지 않아도 되도록 하려면 다음과 같이 하십시오.  
  
-   프로시저에 전달된 매개 변수의 형식을 프로시저 정의에 있는 형식과 일치시킵니다.  
  
-   고유하게 컴파일된 저장 프로시저를 호출하는 경우 이름이 없는 서수 매개 변수를 사용합니다. 가장 효율적으로 실행하려면 명명된 매개 변수를 사용하지 마십시오.  
  
 XEvent `hekaton_slow_parameter_passing`에 `reason=named_parameters`을 사용하면 고유하게 컴파일된 저장 프로시저에 비효율적인 명명된 매개 변수가 사용되었는지 감지할 수 있습니다.  
  
 마찬가지로 동일한 XEvent `hekaton_slow_parameter_passing`에 `reason=parameter_conversion`을 사용하여 일치하지 않는 형식의 사용을 감지할 수 있습니다.  
  
 메모리 최적화 테이블을 사용할 때 많은 시나리오에서 재시도 논리를 구현해야 하며 몇 가지 기능 제한에 대한 문제를 해결해야 하기 때문에 래퍼에서 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 만들어야 할 수 있습니다. 예를 보려면 [Guidelines for Retry Logic for Transactions on Memory-Optimized Tables](memory-optimized-tables.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저](natively-compiled-stored-procedures.md)  
  
  
