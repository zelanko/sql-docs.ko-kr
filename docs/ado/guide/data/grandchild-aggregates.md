---
title: 최하위 집계 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f1bff3c8a155e1e9378acbb659f00817f478382e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47602381"
---
# <a name="grandchild-aggregates"></a>최하위 집계
셰이프 명령의 절에서 생성 된 장 열을 지정할 수 있습니다는 *장-별칭* (일반적으로 사용 하 여 AS 키워드). 장에서 모양의의 모든 열을 식별할 수 있습니다 **레코드 집합** 열이 포함 된 자식을 식별 하는 정규화 된 이름을 사용 합니다. 예를 들어 chap1, 부모 장에서 자식 장에서 chap2, 포함 된 경우 amt amount 열도 포함 다음 정규화 된 이름이 chap1.chap2.amt 표시 됩니다. 그런 다음 정규화 된 이름 (SUM, AVG, MAX, MIN, 개수, STDEV, 또는) 집계 함수 중 하나에 대 한 인수로 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)
