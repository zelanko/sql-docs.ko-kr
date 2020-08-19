---
description: 간격 이스케이프 시퀀스
title: 간격 이스케이프 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2ef792403352568ce5f8d92c07a5b0e1027b507
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483296"
---
# <a name="interval-escape-sequences"></a>간격 이스케이프 시퀀스
ODBC에서는 간격 리터럴에 이스케이프 시퀀스를 사용 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
 {*interval-literal*}  
  
 *Interval 리터럴의*BNF 구문에 대해서는이 부록 뒷부분의 [interval 리터럴 구문](../../../odbc/reference/appendixes/interval-literal-syntax.md) 단원을 참조 하세요.  
  
 간격 리터럴 이스케이프 시퀀스는 데이터 원본에서 간격 데이터 형식이 지원 되는 경우에만 지원 됩니다. 응용 프로그램은 **SQLGetTypeInfo** 를 호출 하 여 이러한 데이터 형식이 지원 되는지 여부를 확인 해야 합니다.
