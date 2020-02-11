---
title: 'Jet: 날짜, 시간 및 타임 스탬프 리터럴 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bb7f0fb02049b6d2f1897c4f495035aee2858f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085488"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: 날짜, 시간, 타임스탬프 리터럴
상호 운용성을 최대화 하기 위해 응용 프로그램은 이스케이프 절 구문을 사용 하 여 ODBC 정식 형식의 날짜 리터럴을 전달 해야 합니다.  
  
-   날짜 리터럴의 경우 {d '*value*'}이 고, 여기서 *선언의*e는 "yyyy-mm-dd" 형식입니다.  
  
-   시간 리터럴의 경우 {t '*value*'}이 고, 여기서 *선언의*e는 "hh: mm: ss" 형식입니다.  
  
 타임 스탬프 리터럴 {ts '*value*'}의 경우 *선언의*e는 "yyyy-mm-dd hh: mm: ss [.f ...]" 형식입니다.
