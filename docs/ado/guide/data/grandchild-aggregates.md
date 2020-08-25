---
description: 최하위 집계
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7215846215db30d31d9a7b54f8e3a3aa2a955a43
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806798"
---
# <a name="grandchild-aggregates"></a>최하위 집계
셰이프 명령의 절에 생성 된 장 열에는 일반적으로 AS 키워드를 사용 하 여 *챕터 별칭 이름을* 지정할 수 있습니다. 열을 포함 하는 자식을 식별 하는 정규화 된 이름을 사용 하 여 모양 있는 **레코드 집합** 의 모든 챕터에 있는 모든 열을 식별할 수 있습니다. 예를 들어, 부모 챕터 chap1에 amount 열인 amt가 있는 자식 장 chap2이 포함 된 경우 정규화 된 이름은 chap1입니다. 그런 다음 정규화 된 이름을 집계 함수 (SUM, AVG, MAX, MIN, COUNT, STDEV 또는 ANY) 중 하나에 대 한 인수로 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 셰이핑 예제](./data-shaping-example.md)