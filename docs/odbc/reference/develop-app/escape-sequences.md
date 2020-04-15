---
title: 이스케이프 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d9589230183b198cb7d59cf9739dab75625441e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298713"
---
# <a name="escape-sequences"></a>이스케이프 시퀀스
ODBC는 날짜, 시간, 타임스탬프 및 날짜 시간 간격 리터럴, 스칼라 함수 호출, **LIKE** 조건자 이스케이프 문자, 외부 조인 및 프로시저 호출에 대한 표준 문법을 포함하는 이스케이프 시퀀스를 정의합니다. 상호 운용 가능한 응용 프로그램은 가능하면 이러한 시퀀스를 사용해야 합니다.  
  
 드라이버가 날짜, 시간, 타임스탬프 또는 날짜 시간 간격 리터럴에 대한 이스케이프 시퀀스를 지원하는지 확인하려면 응용 프로그램이 **SQLGetTypeInfo**를 호출합니다. 데이터 원본이 날짜, 시간, 타임스탬프 또는 날짜 시간 간격 데이터 형식을 지원하는 경우 해당 이스케이프 시퀀스도 지원해야 합니다. 다른 이스케이프 시퀀스가 지원되는지 여부를 확인하려면 응용 프로그램에서 **SQLGetInfo**를 호출합니다.  
  
 자세한 내용은 [ODBC의 이스케이프 시퀀스를](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)참조하세요.
