---
description: 'Jet: 날짜, 시간, 타임스탬프 리터럴'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02b2a7c5c633ee891dbcd962786cb1904bfd5df8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449445"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: 날짜, 시간, 타임스탬프 리터럴
상호 운용성을 최대화 하기 위해 응용 프로그램은 이스케이프 절 구문을 사용 하 여 ODBC 정식 형식의 날짜 리터럴을 전달 해야 합니다.  
  
-   날짜 리터럴의 경우 {d '*value*'}이 고, 여기서 *선언의*e는 "yyyy-mm-dd" 형식입니다.  
  
-   시간 리터럴의 경우 {t '*value*'}이 고, 여기서 *선언의*e는 "hh: mm: ss" 형식입니다.  
  
 타임 스탬프 리터럴 {ts '*value*'}의 경우 *선언의*e는 "yyyy-mm-dd hh: mm: ss [.f ...]" 형식입니다.
