---
title: "이스케이프 시퀀스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1c648549b41ff607ad34175475c6a2b75603625f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="escape-sequences"></a>이스케이프 시퀀스
날짜, 시간, 타임 스탬프 및 날짜/시간 간격 리터럴 스칼라 함수 호출에 대 한 표준 문법을 포함 하는 이스케이프 시퀀스를 정의 하는 ODBC **같은** 이스케이프 문자, 외부 조인 및 프로시저 호출 조건자입니다. 상호 운용 가능한 응용 프로그램 가능 하면 이러한 시퀀스를 사용 해야 합니다.  
  
 드라이버가 날짜, 시간, 타임 스탬프 또는 날짜/시간 간격 리터럴에 대 한 이스케이프 시퀀스를 지 원하는 경우를 확인 하려면 응용 프로그램이 호출 **SQLGetTypeInfo**합니다. 데이터 원본에서 날짜, 시간, 타임 스탬프 또는 datetime 간격 데이터 형식의 지 원하는 경우 또한 해당 이스케이프 시퀀스를 지원 해야 합니다. 다른 이스케이프 시퀀스는 지원 여부를 확인 하려면 응용 프로그램이 호출 **SQLGetInfo**합니다.  
  
 자세한 내용은 참조 [odbc에서 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)이 섹션의 뒷부분에 나오는 합니다.

