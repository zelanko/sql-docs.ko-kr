---
title: 최하위 집계 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 589bece101c52a38d11f10a5d5f8f162aa3af8ad
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="grandchild-aggregates"></a>최하위 집계
Shape 명령의 절에 만든 장 열을 지정할 수 있습니다는 *장 별칭 이름* 일반적으로 (AS 키워드)를 사용 합니다. 모양을 장에서 열을 식별할 수 있습니다 **레코드 집합** 열이 포함 된 자식을 식별 하는 정규화 된 이름을 사용 합니다. 예를 들어 chap1, 부모 장에서 자식 장, chap2, 포함 하에 amt amount 열 경우 정규화 된 이름이 chap1.chap2.amt 표시 됩니다. 다음 정규화 된 이름 (SUM, AVG, MAX, MIN, COUNT, STDEV, 또는 모든) 집계 함수 중 하나에 대 한 인수로 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)
