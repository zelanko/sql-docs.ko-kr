---
title: 프로시저 실행 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98c36f02bde63862748eef14a8cbae063ca4e472
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069950"
---
# <a name="executing-procedures"></a>프로시저 실행
ODBC는 프로시저 실행을 위한 표준 이스케이프 시퀀스를 정의 합니다. 이 시퀀스의 구문과이 시퀀스를 사용 하는 코드 예제는 [프로시저 호출](../../../odbc/reference/develop-app/procedure-calls.md)을 참조 하세요.  
  
 프로시저를 실행 하기 위해 응용 프로그램은 다음 작업을 수행 합니다.  
  
1.  매개 변수의 값을 설정 합니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요.  
  
2.  **Sqlexecdirect** 를 호출 하 고 프로시저를 실행 하는 SQL 문을 포함 하는 문자열을 전달 합니다. 이 문은 ODBC 또는 DBMS 관련 구문으로 정의 된 이스케이프 시퀀스를 사용할 수 있습니다. DBMS 관련 구문을 사용 하는 문은 상호 운용할 수 없습니다.  
  
3.  **Sqlexecdirect** 를 호출 하는 경우 드라이버는 다음과 같습니다.  
  
    -   현재 매개 변수 값을 검색 하 고 필요에 따라 변환 합니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요.  
  
    -   데이터 소스의 프로시저를 호출 하 고 변환 된 매개 변수 값을 보냅니다. 드라이버가 프로시저를 호출 하는 방법은 드라이버와 관련 됩니다. 예를 들어 데이터 원본의 SQL 문법을 사용 하 고이 문을 실행을 위해 제출 하도록 SQL 문을 수정 하거나, DBMS의 데이터 스트림 프로토콜에 정의 된 RPC (원격 프로시저 호출) 메커니즘을 사용 하 여 직접 프로시저를 호출할 수 있습니다.  
  
    -   프로시저를 성공적으로 수행 한다고 가정 하 고 모든 입력/출력 또는 출력 매개 변수 값 또는 프로시저 반환 값을 반환 합니다. 프로시저에서 생성 된 다른 모든 결과 (행 개수 및 결과 집합)가 처리 될 때까지 이러한 값을 사용 하지 못할 수도 있습니다. 프로시저가 실패 하면 드라이버에서 오류를 반환 합니다.
