---
title: 모범 사례- 고유하게 컴파일된 저장 프로시저
description: 애플리케이션에서 성능이 중요한 부분에 일반적으로 사용되는 고유하게 컴파일된 저장 프로시저 모범 사례에 대해 알아봅니다.
ms.custom: seo-dt-2019
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694b
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bc9fffa0c2b916163e0b9e8698cdf1f7df59667a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723387"
---
# <a name="best-practices-for-calling-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저를 호출하는 최선의 구현 방법
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
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
  
 XEvent **natively_compiled_proc_slow_parameter_passing**을 사용하여 고유하게 컴파일된 저장 프로시저에서 비효율적인 매개 변수를 감지할 수 있습니다.
 - 일치하지 않는 형식: **reason=parameter_conversion**
 - 명명된 매개 변수: **reason=named_parameters**
 - DEFAULT 값: **reason=default** 
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
