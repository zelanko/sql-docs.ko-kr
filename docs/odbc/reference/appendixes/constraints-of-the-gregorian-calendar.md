---
title: 일반 달력의 제약 조건 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30fbdd17e7ec5eb970948e1c7133020081222614
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847931"
---
# <a name="constraints-of-the-gregorian-calendar"></a>일반 달력의 제약 조건
Date 및 datetime 데이터 형식 및 간격 데이터 형식의 필드를 후행 일반 달력의 제약 조건에 맞아야 합니다. 이러한 제약 조건은 아래와 같습니다.  
  
-   월 필드의 값은 1에서 12 사이 여야 합니다.  
  
-   일 필드의 값 1에서 월의 일 수가 까지의 범위에 있어야 합니다. 월의 일 수가 연도 및 월 필드의 값에서 결정 됩니다 및 28, 29, 30 또는 31 일 수 있습니다. (월의 일 수가 연도가 윤년 인지 여부에 달라질 수 있습니다.)  
  
-   시간 필드의 값은 0에서 23 사이 사이 여야 합니다.  
  
-   분 필드의 값은 0에서 59 사이 사이 여야 합니다.  
  
-   간격 데이터 형식의 후행 시간 (초) 필드에 대 한 시간 (초) 필드의 값은 0과 59.9 사이 여야 합니다 (*n*), inclusive, 여기서 *n* 초 소수 부분 자릿수의 숫자입니다.  
  
-   Datetime 데이터 형식의 후행 시간 (초) 필드에 대 한 시간 (초) 필드의 값은 0에서 61.9 사이 여야 합니다 (*n*), inclusive, 여기서 *n* "9" 자릿수 및 값 지정 *n*  소수 자릿수 초의 전체 자릿수입니다. (시간 (초) 범위 sidereal 시간 동기화를 유지 하려면 최대 2 초의 윤 초가 허용 합니다.)
