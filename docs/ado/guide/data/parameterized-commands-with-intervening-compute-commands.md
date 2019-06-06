---
title: 매개 변수가 있는 중간 계산 명령 사용 하 여 명령 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
- APPEND clause [ADO]
- COMPUTE command [ADO]
ms.assetid: 732f624f-8900-4608-9815-194302d22e8b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b33feb8075babd50f67b6c01da5afadcd1c33e0b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700514"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>중간에 COMPUTE 명령을 사용한 매개 변수화된 명령
일반적으로 매개 변수가 있는 shape 추가 명령에 부모 만드는 절 **Recordset** 쿼리 명령 및 자식 만드는 다른 절을 사용 하 여 **레코드 집합** 매개 변수가 있는 쿼리 명령- 즉, 매개 변수 자리 표시자를 포함 하는 명령 (물음표를 "?"). 결과 셰이핑 **레코드 집합** 부모는 상위 수준 차지 두 수준 있고 자식 하위 수준을 차지 합니다.  
  
 절을 만드는 자식 **레코드 집합** 수는 임의 개수의 중첩된 셰이프 계산 명령 가장 깊이 중첩 된 명령에서 매개 변수가 있는 쿼리를 포함 하는 위치입니다. 결과 셰이핑 **레코드 집합** 부모 최상위 수준 차지 하는 여러 수준에는 최하위 수준 및 임의 개수의 자식 차지 **레코드 집합**s에서 생성 합니다 명령에는 중간 수준 차지합니다.  
  
 중간 만들려면 명령을 그룹화 기능 shapeCOMPUTE 확인 하 고 집계 함수를 호출 하는이 기능에 대 한 일반적인 용도 **Recordset** 자식에 대 한 분석 정보를 사용 하 여 개체 **레코드 집합** . 또한 매개 변수가 있는 모양 명령을 이기 때문에 각 시간 부모 장 열에 액세스할 새 자식 **레코드 집합** 검색 될 수 있습니다. 중간 수준 자식에서 파생 되므로, 이러한도 다시 계산 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)
