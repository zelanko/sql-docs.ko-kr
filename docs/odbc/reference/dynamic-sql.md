---
title: 동적 SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cbecd1d6db1d5ed77082253f6a6a57a96ceec4d1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748410"
---
# <a name="dynamic-sql"></a>동적 SQL
정적 SQL 다양 한 상황에서 잘 작동 하지만 클래스는 데이터 액세스를 확인할 수 없는 사전에 응용 프로그램에 있습니다. 예를 들어 스프레드시트에는 사용자가 스프레드시트 보냅니다 dbms 데이터를 검색할 쿼리를 입력 하도록 허용 합니다. 이 쿼리의 내용은 분명히 알 수 없으므로 프로그래머에 게 스프레드시트 프로그램 기록 되는 경우.  
  
 이 문제를 해결 하기 위해 스프레드시트 동적 SQL을 호출 하는 포함 된 SQL의 형태를 사용 합니다. 프로그램에 하드 코딩 되어, 정적 SQL 문을 달리에 동적 SQL 문의 런타임에 작성 하 고 문자열 호스트 변수에 배치 될 수 있습니다. 그런 다음 처리를 위해 DBMS에 전송 됩니다. DBMS 런타임에 동적 SQL 문에 대 한 액세스 계획을 생성 해야 하기 때문에 동적 SQL은 일반적으로 정적 SQL 보다 느립니다. 동적 SQL 문을 포함 하는 프로그램을 컴파일할 때 정적 SQL 처럼 프로그램에서 동적 SQL 문은 제거 되지 됩니다. 대신, DBMS; 문을 전달 하는 함수 호출으로 대체 됩니다. 정적 SQL 문은 동일한 프로그램에서 일반적으로 처리 됩니다.  
  
 즉시 실행 문을 사용 하 여 간단 하 게 동적 SQL 문을 실행할 경우 이 문은 컴파일 및 실행에 대 한 dbms SQL 문에 전달합니다.  
  
 즉시 실행 문의 한 단점은 DBMS 각 문이 실행 될 때마다 SQL 문 처리의 다섯 단계를 통과 해야입니다. 이 프로세스에 관련 된 오버 헤드는 많은 문을 동적으로 실행 되 고 불필요 해당 문도 이와 비슷합니다 경우 중요할 수 있습니다. 동적 SQL이이 문제를 해결 하려면 다음 단계를 사용 하 여 준비 된 실행을 호출 하는 실행의 를 제공 합니다.  
  
1.  프로그램을 즉시 실행 문에 대 한 것 처럼 버퍼에서 SQL 문을 생성 합니다. 호스트 변수 대신 상수 값을 나중에 제공 됩니다 나타내기 위해 문 텍스트의 아무 곳 이나 상수에 대 한 물음표 (?)를 대체할 수 있습니다. 물음표는 매개 변수 표식으로 호출 됩니다.  
  
2.  프로그램 DBMS는 DBMS 구문 분석, 유효성 검사 및 문을 최적화 하 고 실행을 생성 하는 요청에 대 한 계획, 준비 문 사용 하 여 SQL 문을 전달 합니다. 프로그램 다음 EXECUTE 문을 (없습니다: 즉시 실행 문)를 사용 하 여 나중에 준비 문을 실행 합니다. SQL 데이터 영역 또는 SQLDA 라는 특수 한 데이터 구조를 통해 문에 대 한 매개 변수 값을 전달 합니다.  
  
3.  프로그램 EXECUTE 문을 반복적으로 사용할 수, 동적 문이 실행 될 때마다 다른 매개 변수 값을 제공 합니다.  
  
 준비 된 실행 되지 여전히 정적 SQL와 동일 합니다. 정적 SQL, SQL 문 처리의 처음 네 단계를 수행 컴파일 시 됩니다. 준비 된 실행을 계속 수행 런타임 시 이러한 단계 있지만 한 번만 수행 되 실행 계획의 실행 이라고 하는 경우에 수행이 됩니다. 이 동적 SQL의 아키텍처에 내재 된 성능 단점 중 일부를 제거할 수 있습니다. 다음 그림은 정적 SQL, 즉시 실행을 사용 하 여 동적 SQL 및 준비 된 실행을 사용 하 여 동적 SQL의 차이점을 보여 줍니다.
