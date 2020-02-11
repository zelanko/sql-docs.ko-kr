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
ms.openlocfilehash: d73282cde4d0598d7e6a35ac6273935626b96969
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68001375"
---
# <a name="escape-sequences"></a>이스케이프 시퀀스
ODBC는 날짜, 시간, 타임 스탬프 및 날짜/시간 간격 리터럴, 스칼라 함수 호출 **(예: 조건자 이스케이프** 문자, 외부 조인 및 프로시저 호출)에 대 한 표준 문법을 포함 하는 이스케이프 시퀀스를 정의 합니다. 상호 운용 가능한 응용 프로그램은 가능 하면 항상 이러한 시퀀스를 사용 해야 합니다.  
  
 드라이버가 날짜, 시간, 타임 스탬프 또는 datetime 간격 리터럴에 대 한 이스케이프 시퀀스를 지원 하는지 확인 하기 위해 응용 프로그램은 **SQLGetTypeInfo**를 호출 합니다. 데이터 원본에서 날짜, 시간, 타임 스탬프 또는 datetime interval 데이터 형식이 지원 되는 경우에도 해당 이스케이프 시퀀스를 지원 해야 합니다. 다른 이스케이프 시퀀스가 지원 되는지 여부를 확인 하기 위해 응용 프로그램은 **SQLGetInfo**를 호출 합니다.  
  
 자세한 내용은이 섹션의 뒷부분에 나오는 [ODBC의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)를 참조 하세요.
