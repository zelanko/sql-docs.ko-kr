---
title: "동적 SQL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4c24d1dbab68a1e47b5dfe7b48dc3df86fb9f692
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="dynamic-sql"></a>동적 SQL
다양 한 상황에서 잘 작동 하는 정적 SQL 이지만 한 응용 프로그램에는 데이터 액세스 확인할 수 없는 사전에 있습니다. 예를 들어 스프레드시트 스프레드시트 보냅니다는 DBMS에 데이터를 검색 하는 쿼리를 입력할 수 있습니다. 이 쿼리 내용 분명히 알 수 없으므로 프로그래머에 게 스프레드시트 프로그램 기록 되는 경우.  
  
 이 문제를 해결 하기 위해 스프레드시트 동적 SQL을 호출 하는 포함 된 SQL의 형태를 사용 합니다. 프로그램에 하드 코딩 되어, 정적 SQL 문을 달리 동적 SQL 문 실행 시 빌드하고 수 문자열 호스트 변수에 배치 합니다. 그런 다음 처리를 위해 DBMS에 전송 됩니다. DBMS 동적 SQL 문의 실행 시에 액세스 계획을 생성 해야 하므로 동적 SQL 정적 SQL 보다 일반적으로 느립니다. 동적 SQL 문이 포함 된 프로그램을 컴파일할 때 동적 SQL 문의 정적 SQL에서와 같이 프로그램에서 제거 되지 않습니다. 대신, DBMS; 문을 전달 하는 함수 호출으로 대체 됩니다. 동일한 프로그램에서 정적 SQL 문은 정상적으로 처리 됩니다.  
  
 즉시 실행 문을 사용 하 여 동적 SQL 문을 실행 하는 가장 간단한 방법은 됩니다. 이 문은 컴파일 및 실행을 위한 DBMS에 SQL 문을 전달합니다.  
  
 한 가지 즉시 실행 문의 단점은 DBMS 각 문이 실행 될 때마다 SQL 문 처리의 5 단계를 통과 해야 합니다. 이 프로세스에 관련 된 오버 헤드는 많은 문을 동적으로 실행 되 고 이러한 문을 비슷한 경우 낭비은 중요할 수 있습니다. 동적 SQL이이 문제를 해결 하려면 다음 단계를 사용 하 여 준비 된 실행을 호출 하는 실행의 ´ ù를 제공 합니다.  
  
1.  프로그램 즉시 실행 문에 대 한와 마찬가지로 버퍼에는 SQL 문을 생성 합니다. 호스트 변수 대신 물음표 (?) 상수에 대 한 값을 나중에 제공 됩니다 나타내기 위해 문 텍스트의 상수에 대 한 데이터를 대체할 수 있습니다. 매개 변수는 매개 변수 표식으로 호출 됩니다.  
  
2.  프로그램은 DBMS 구문 분석, 유효성 검사, 및 문을 최적화 하 고 실행을 생성 하는 요청에 대 한 계획 준비 문으로 DBMS에 SQL 문을 전달 합니다. 다음 프로그램 (즉시 실행 문 하지) EXECUTE 문을 사용 하 여 나중에 준비 문을 실행 하 합니다. SQL 데이터 영역 또는 잘못 된 특수 한 데이터 구조를 통해 문에 대 한 매개 변수 값을 전달 합니다.  
  
3.  프로그램 문을 사용 하 여 EXECUTE 반복 해 서 동적 문이 실행 될 때마다 다른 매개 변수 값을 제공 합니다.  
  
 준비 된 실행이 여전히 정적 SQL와 동일 합니다. 정적 SQL SQL 문 처리의 처음 네 단계 수행 컴파일 타임에 됩니다. 준비 된 실행에서 아직 수행 런타임 시 이러한 단계 하지만; 한 번만 수행 됩니다. 실행 계획의 EXECUTE를 호출할 때에 수행이 됩니다. 이 동적 SQL의 아키텍처에 내재 된 성능 단점 중 일부를 제거할 수 있습니다. 다음 그림은 정적 SQL, 동적 SQL로 즉시 실행 및 동적 SQL로 준비 된 실행 간의 차이점을 보여 줍니다.
