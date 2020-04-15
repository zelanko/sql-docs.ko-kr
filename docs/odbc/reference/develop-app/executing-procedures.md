---
title: 절차 실행 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a796c615d7dfdec11a9acb90ab4b5129cf69717
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305714"
---
# <a name="executing-procedures"></a>프로시저 실행
ODBC는 프로시저 실행에 대한 표준 이스케이프 시퀀스를 정의합니다. 이 시퀀스의 구문및 이를 사용하는 코드 예제는 [프로시저 호출](../../../odbc/reference/develop-app/procedure-calls.md)을 참조하십시오.  
  
 프로시저를 실행하기 위해 응용 프로그램은 다음 작업을 수행합니다.  
  
1.  매개 변수의 값을 설정합니다. 자세한 내용은 이 섹션의 다음 부분의 [문 매개 변수를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.  
  
2.  **SQLExecDirect를** 호출하고 프로시저를 실행하는 SQL 문이 포함된 문자열을 전달합니다. 이 문은 ODBC 또는 DBMS 관련 구문으로 정의된 이스케이프 시퀀스를 사용할 수 있습니다. DBMS 관련 구문을 사용하는 문은 상호 운용할 수 없습니다.  
  
3.  **SQLExecDirect가** 호출되면 드라이버:  
  
    -   현재 매개 변수 값을 검색하고 필요에 따라 변환합니다. 자세한 내용은 이 섹션의 다음 부분의 [문 매개 변수를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.  
  
    -   데이터 원본의 프로시저를 호출하고 변환된 매개 변수 값을 보냅니다. 드라이버가 프로시저를 호출하는 방법은 드라이버에 따라 다릅니다. 예를 들어 데이터 원본의 SQL 문법을 사용하고 실행을 위해 이 문을 제출하도록 SQL 문을 수정하거나 DBMS의 데이터 스트림 프로토콜에 정의된 RPC(원격 프로시저 호출) 메커니즘을 사용하여 프로시저를 직접 호출할 수 있습니다.  
  
    -   프로시저가 성공한다고 가정하면 입력/출력 또는 출력 매개 변수 또는 프로시저 반환 값의 값을 반환합니다. 프로시저에서 생성된 다른 모든 결과(행 개수 및 결과 집합)가 처리될 때까지 이러한 값을 사용하지 못할 수 있습니다. 프로시저가 실패하면 드라이버는 오류를 반환합니다.
