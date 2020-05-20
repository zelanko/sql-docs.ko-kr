---
title: 중간 계산 명령이 포함 된 매개 변수가 있는 명령 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f66bde29a5036ed671f9af17bf5aab1df4acbca
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764784"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>중간에 COMPUTE 명령을 사용한 매개 변수화된 명령
매개 변수가 있는 일반적인 shape APPEND 명령에는 쿼리 명령을 사용 하 여 부모 **레코드 집합** 을 만드는 절과 매개 변수가 있는 쿼리 명령, 즉 매개 변수 자리 표시자 (물음표, "?")가 포함 된 명령이 포함 된 하위 **레코드 집합** 을 만드는 다른 절이 있습니다. 결과를 생성 하는 **레코드 집합** 에는 부모가 상위 수준으로 차지 하 고 자식은 하위 수준을 차지 하는 두 가지 수준이 있습니다.  
  
 자식 **레코드 집합** 을 만드는 절은 이제 가장 깊게 중첩 된 명령에 매개 변수가 있는 쿼리를 포함 하는 중첩 된 shape 계산 명령의 임의 수를 사용할 수 있습니다. 결과 **레코드 집합** 에는 부모가 최상위 수준으로 차지 하 고, 자식이 lowermost 수준을 차지 하며, 셰이프 계산 명령에 의해 생성 되는 임의 개수의 **레코드 집합이**중간 수준에 포함 되는 여러 수준이 있습니다.  
  
 이 기능을 사용 하는 일반적인 방법은 shapeCOMPUTE 명령의 집계 함수 및 그룹화 기능을 호출 하 여 하위 **레코드 집합**에 대 한 분석 정보를 포함 하는 중간 **레코드 집합** 개체를 만드는 것입니다. 또한이는 매개 변수가 있는 shape 명령 이므로 부모의 장 열에 액세스할 때마다 새 자식 **레코드 집합** 을 검색할 수 있습니다. 중간 수준이 자식에서 파생 되기 때문에 다시 계산 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)
