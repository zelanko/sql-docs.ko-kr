---
title: 일반 달력의 제약 조건 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Gregorian calendar
- Gregorian calendar [ODBC]
ms.assetid: 70667410-c582-4369-8e06-9d98e21cd2bf
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cea1f4b4dd5b56feee64623bd6ff2355ce4332c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="constraints-of-the-gregorian-calendar"></a>일반 달력의 제약 조건
Date 및 datetime 데이터 형식 및 간격 데이터 형식의 후행 필드는 일반 달력의 제약 조건에 따라야 합니다. 이러한 제약 조건은 다음과 같습니다.  
  
-   월 필드의 값은 1에서 12 사이 여야 합니다.  
  
-   일 필드의 값 1에서 월의 일 수가 까지의 범위에 있어야 합니다. 연도 및 월 필드의 값에서 결정 하 고 28 이나 29, 30, 31 일 수 있습니다 하는 월의 일 수입니다. (월의 일 수가 윤년 인지 여부에 달라질 수 있습니다.)  
  
-   시간 필드의 값은 0에서 23 사이 사이 여야 합니다.  
  
-   분 필드의 값은 0에서 59 사이의 사이 여야 합니다.  
  
-   후행 초 필드의 간격 데이터 형식의 경우 초 필드의 값은 0과 59.9 사이 여야 합니다 (*n*) (포함), 여기서 *n* 초 소수 부분 자릿수의 숫자의 수입니다.  
  
-   후행 초 필드의 날짜/시간 데이터 형식의 경우 초 필드의 값은 0에서 61.9 사이 여야 합니다 (*n*) (포함), 여기서 *n* "9" 자리 숫자를 지정 하는 값을 *n*  소수 자릿수 초의 전체 자릿수입니다. (초의 범위 sidereal 시간 동기화를 유지 하려면 최대 2 초의 윤 초가 허용 합니다.)
