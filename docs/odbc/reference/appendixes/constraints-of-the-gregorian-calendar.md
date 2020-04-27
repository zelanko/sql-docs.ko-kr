---
title: 양력 달력의 제약 조건 | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284763"
---
# <a name="constraints-of-the-gregorian-calendar"></a>일반 달력의 제약 조건
날짜 및 날짜/시간 데이터 형식과 interval 데이터 형식의 후행 필드는 양력의 제약 조건을 준수 해야 합니다. 이러한 제약 조건은 다음과 같습니다.  
  
-   월 필드의 값은 1에서 12 (포함) 사이 여야 합니다.  
  
-   일 필드의 값은 1에서 해당 월의 일 수 사이의 범위에 있어야 합니다. 월의 일 수는 연도 및 월 필드의 값을 기준으로 결정 되며 28, 29, 30 또는 31 일 수 있습니다. (해당 월의 일 수는 윤년 인지에 따라 달라질 수도 있습니다.)  
  
-   시간 필드의 값은 0에서 23 (포함) 사이 여야 합니다.  
  
-   분 필드의 값은 0에서 59 (포함) 사이 여야 합니다.  
  
-   Interval 데이터 형식의 후행 초 필드에 대해 초 필드의 값은 0에서 59.9 (*n*) 사이 여야 합니다. 여기서 *n* 은 초 소수 부분 자릿수의 자릿수입니다.  
  
-   Datetime 데이터 형식의 후행 초 필드에 대해 seconds 필드의 값은 0에서 61.9 (*n*) 사이 여야 합니다. 여기서 *n* 은 "9"의 숫자를 지정 하 고 *n* 의 값은 초 소수 부분 자릿수입니다. 초 범위는 sidereal 시간 동기화를 유지 하기 위해 두 개의 윤 초를 허용 합니다.
