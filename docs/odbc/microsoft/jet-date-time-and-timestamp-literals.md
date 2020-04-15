---
title: '제트기: 날짜, 시간 및 타임스탬프 리터럴 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 372b7c1dab1ad8ff000fb88729c3b02e05d4a21c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299940"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: 날짜, 시간, 타임스탬프 리터럴
상호 운용성을 극대화하기 위해 응용 프로그램은 escape 절 구문을 사용하여 ODBC 표준 형식으로 날짜 리터럴을 전달해야 합니다.  
  
-   날짜 리터럴의 경우 {d *'value*'}, *valu*e가 "yyyy-mm-dd" 형식인 경우  
  
-   시간 리터럴의 경우 {t *'value*'}, *valu*e가 "hh:mm:ss" 형태로 있는 경우  
  
 타임스탬프 리터럴의 경우 {ts *'value'},* *valu*e가 "yyyy-mm-dd hh:mm:ss[.f...]"라는 형태로 되어 있습니다.
