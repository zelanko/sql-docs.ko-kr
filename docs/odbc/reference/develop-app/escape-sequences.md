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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1423d7bcc0f0b943b490fdcf8f931efb6b533c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259273"
---
# <a name="escape-sequences"></a>이스케이프 시퀀스
날짜, 시간, 타임 스탬프 및 날짜/시간 간격 리터럴 스칼라 함수 호출에 대 한 표준 문법을 포함 하는 이스케이프 시퀀스를 정의 하는 ODBC **같은** 조건자 이스케이프 문자, 외부 조인 및 프로시저 호출 합니다. 상호 운용 가능한 응용 프로그램 가능 하면 이러한 시퀀스를 사용 해야 합니다.  
  
 드라이버가 날짜, 시간, 타임 스탬프 또는 날짜/시간 간격 리터럴에 대 한 이스케이프 시퀀스를 지 원하는 경우를 확인 하려면 응용 프로그램 호출 **SQLGetTypeInfo**합니다. 데이터 원본에서 날짜, 시간, 타임 스탬프 또는 datetime 간격 데이터 형식을 지 원하는 경우 해당 이스케이프 시퀀스에도 지원 해야 합니다. 응용 프로그램이 호출 다른 이스케이프 시퀀스가 지원 되는지 여부를 결정할 **SQLGetInfo**합니다.  
  
 자세한 내용은 [ODBC의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)이 섹션의 뒷부분에 나오는.
