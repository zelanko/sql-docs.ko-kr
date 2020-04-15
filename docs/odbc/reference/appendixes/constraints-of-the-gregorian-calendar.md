---
title: 그레고리오 력의 제약 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Gregorian calendar
- Gregorian calendar [ODBC]
ms.assetid: 70667410-c582-4369-8e06-9d98e21cd2bf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f88842c7426e17af1fdc0533b8b97e2c559de237
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284763"
---
# <a name="constraints-of-the-gregorian-calendar"></a>일반 달력의 제약 조건
날짜 및 날짜 시간 데이터 형식 및 간격 데이터 형식의 후행 필드는 [이] [이]의 제약 조건을 준수해야 합니다. 이러한 제약 조건은 다음과 같습니다.  
  
-   월 필드의 값은 1에서 12 사이여야 합니다(포함).  
  
-   일 필드의 값은 1부터 월의 일 수까지의 범위여야 합니다. 월의 일 수는 연도 및 월 필드의 값에서 결정되며 28, 29, 30 또는 31일 수 있습니다. (월의 일 수도 윤년인지 여부에 따라 달라질 수 있습니다.)  
  
-   시간 필드의 값은 0에서 23 사이여야 합니다(포함).  
  
-   미닛 필드의 값은 0에서 59 사이여야 합니다( 포함).  
  
-   간격 데이터 형식의 후행 초 필드의 경우 초 필드의 값은 0에서 59.9(n) 사이여야 하며, 여기서 *n은* 소수 초 정밀도의 숫자 수입니다.*n*  
  
-   datetime 데이터 형식의 후행 초 필드의 경우 초 필드의 값은 0에서 61.9(n) 사이여야 하며, 여기서 *n은* "9" 자릿수를 지정하고 *n값은* 분수 초 정밀도입니다.*n* (초 범위는 사이드리얼 타임의 동기화를 유지하기 위해 최대 2개의 윤초를 허용합니다.)
