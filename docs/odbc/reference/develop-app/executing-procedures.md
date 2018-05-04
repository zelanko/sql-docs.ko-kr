---
title: 프로시저 실행 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c3eb4c4106eebe3fc63207f7029518df6afc457f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="executing-procedures"></a>프로시저 실행
ODBC는 프로시저를 실행 하기 위한 표준 이스케이프 시퀀스를 정의 합니다. 이 시퀀스 및이 사용 하는 코드 예제에서는 구문에 대 한 참조 [프로시저 호출](../../../odbc/reference/develop-app/procedure-calls.md)합니다.  
  
 프로시저를 실행 하려면 응용 프로그램에서는 다음 작업을 수행 합니다.  
  
1.  매개 변수 값을 설정합니다. 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)이 섹션의 뒷부분에 나오는 합니다.  
  
2.  호출 **SQLExecDirect** 프로시저를 실행 하는 SQL 문을 포함 하는 문자열을 전달 합니다. 이 문은 ODBC 또는 DBMS 관련 구문을 사용 합니다;으로 정의 된 이스케이프 시퀀스를 사용할 수 있습니다. DBMS 관련 구문을 사용 하는 문을 상호 운용 되지는 않습니다.  
  
3.  때 **SQLExecDirect** 호출 되는 드라이버:  
  
    -   현재 매개 변수 값을 검색 하 고 필요에 따라 변환 합니다. 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)이 섹션의 뒷부분에 나오는 합니다.  
  
    -   데이터 원본에 프로시저를 호출 하 고 변환 된 매개 변수 값을 보냅니다. 드라이버 관련은 드라이버는 프로시저를 호출 하는 방법입니다. 예를 들어 로그 분석은 데이터 소스의 SQL 문법을 사용 하 고 실행 하기 위해이 문을 제출 하는 SQL 문을 수정할 수 있습니다 또는 DBMS의 데이터 스트림 프로토콜에 정의 된 원격 프로시저 호출 (RPC) 메커니즘을 사용 하 여 직접 프로시저를 호출할 수 있습니다.  
  
    -   모든 입/출력 또는 출력 매개 변수의 값 또는 프로시저가 성공할 것으로 가정 하 여 프로시저 반환 값을 반환 합니다. 다른 모든 결과 (행 개수 및 결과 집합) 생성 프로시저에 의해 처리 된 후 이러한 값 수까지 사용할 수 없습니다. 프로시저가 실패할 경우 드라이버는 모든 오류를 반환 합니다.
