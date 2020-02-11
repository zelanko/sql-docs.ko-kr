---
title: 손자 집계 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac0b06479b3ad4feedaa63bdac227d028b7a9e09
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925234"
---
# <a name="grandchild-aggregates"></a>최하위 집계
셰이프 명령의 절에 생성 된 장 열에는 일반적으로 AS 키워드를 사용 하 여 *챕터 별칭 이름을* 지정할 수 있습니다. 열을 포함 하는 자식을 식별 하는 정규화 된 이름을 사용 하 여 모양 있는 **레코드 집합** 의 모든 챕터에 있는 모든 열을 식별할 수 있습니다. 예를 들어, 부모 챕터 chap1에 amount 열인 amt가 있는 자식 장 chap2이 포함 된 경우 정규화 된 이름은 chap1입니다. 그런 다음 정규화 된 이름을 집계 함수 (SUM, AVG, MAX, MIN, COUNT, STDEV 또는 ANY) 중 하나에 대 한 인수로 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)
