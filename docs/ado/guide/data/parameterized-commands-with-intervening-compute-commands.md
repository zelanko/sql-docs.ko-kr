---
title: "매개 변수가 있는 중간 계산 명령 사용 하 여 명령 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
- APPEND clause [ADO]
- COMPUTE command [ADO]
ms.assetid: 732f624f-8900-4608-9815-194302d22e8b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8821ebd2fb20cf32c6b1921c36e45404421f415b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>중간으로 매개 변수화 된 명령을 계산 명령
일반적으로 매개 변수가 있는 shape APPEND 명령에는 부모 만드는 **레코드 집합** 쿼리 명령 및 절 자식 **레코드 집합** 매개 변수가 있는 쿼리 명령- 즉, 매개 변수 자리 표시자를 포함 하는 명령 (매개 변수 "?"). 명령의 결과로 만들어지는 셰이핑된 **레코드 집합** 부모는 상위 수준 차지 하는 두 개의 수준이 및 자식 하위 수준을 차지 합니다.  
  
 자식 만드는 절 **레코드 집합** 가능한 한 빨리 전체 임의 개수의 중첩 된 모양 명령, 가장 깊이 중첩 된 명령에서 매개 변수가 있는 쿼리를 포함 하는 위치입니다. 명령의 결과로 만들어지는 셰이핑된 **레코드 집합** 매개 변수가 있는 부모 차지 최상위 수준, 최하위 수준 및 임의 개수의 자식 차지 **레코드 집합**s에 의해 생성 된는 중간 수준 차지 하는 명령입니다.  
  
 장애가 만들려고 명령을 shapeCOMPUTE의 그룹화 성능과 집계 함수를 호출 하는이 기능에 대해 사용 하는 일반적인 **레코드 집합** 자식에 대 한 분석 정보를 사용 하 여 개체 **레코드 집합** . 또한 매개 변수가 있는 shape 명령 이기 때문에 될 때마다 부모 장 열에 액세스 하는 새 자식 **레코드 집합** 검색 될 수 있습니다. 중첩 된 자식에서 파생 되므로은 또한 다시 계산 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)

