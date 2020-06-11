---
title: 동적 SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa4ac69602761f7c2a8d28e56db76bbfc39fc753
ms.sourcegitcommit: dc6ea6665cd2fb58a940c722e86299396b329fec
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84423257"
---
# <a name="dynamic-sql"></a>동적 SQL
정적 SQL은 많은 상황에서 잘 작동 하지만 데이터 액세스를 미리 확인할 수 없는 응용 프로그램 클래스가 있습니다. 예를 들어 스프레드시트를 사용 하 여 스프레드시트에서 데이터를 검색 하기 위해 DBMS로 보내는 쿼리를 입력할 수 있습니다. 스프레드시트 프로그램을 작성할 때 프로그래머에 게이 쿼리의 내용을 명확히 알 수 없습니다.  
  
 이 문제를 해결 하기 위해 스프레드시트는 동적 SQL 이라고 하는 포함 된 SQL의 형태를 사용 합니다. 프로그램에 하드 코딩 된 정적 SQL 문과 달리 동적 SQL 문은 런타임에 빌드하고 문자열 호스트 변수에 배치할 수 있습니다. 그런 다음 처리를 위해 DBMS에 전송 됩니다. DBMS는 런타임에 동적 SQL 문에 대 한 액세스 계획을 생성 해야 하므로 동적 SQL은 일반적으로 정적 SQL 보다 느립니다. 동적 SQL 문을 포함 하는 프로그램을 컴파일하는 경우 동적 sql 문은 정적 SQL과 같이 프로그램에서 제거 되지 않습니다. 대신, 문을 DBMS에 전달 하는 함수 호출로 대체 됩니다. 같은 프로그램의 정적 SQL 문은 정상적으로 처리 됩니다.  
  
 동적 SQL 문을 실행 하는 가장 간단한 방법은 EXECUTE 즉각적인 문을 사용 하는 것입니다. 이 문은 컴파일 및 실행을 위해 SQL 문을 DBMS에 전달 합니다.  
  
 EXECUTE 즉각적인 문의 한 가지 단점은 DBMS가 문을 실행할 때마다 SQL 문을 처리 하는 5 단계를 각각 수행 해야 한다는 것입니다. 많은 문이 동적으로 실행 되는 경우이 프로세스와 관련 된 오버 헤드는 매우 중요할 수 있으며, 해당 문이 비슷한 경우에는 불필요 합니다. 이러한 상황을 해결 하기 위해 동적 SQL은 다음 단계를 사용 하 여 준비 된 실행 이라는 최적화 된 형태의 실행을 제공 합니다.  
  
1.  프로그램은 EXECUTE 즉각적인 문과 마찬가지로 SQL 문을 버퍼에 생성 합니다. 호스트 변수 대신 물음표 (?)를 문 텍스트의 임의 위치에 대체 하 여 상수 값이 나중에 제공 된다는 것을 나타낼 수 있습니다. 물음표는 매개 변수 표식으로 호출 됩니다.  
  
2.  프로그램은 문을 구문 분석, 유효성 검사 및 최적화 하도록 요청 하 고이에 대 한 실행 계획을 생성 하도록 요청 하는 PREPARE 문으로 SQL 문을 DBMS에 전달 합니다. 그런 다음 프로그램은 execute 문 (EXECUTE 즉각적인 문이 아님)을 사용 하 여 나중에 준비 문을 실행 합니다. SQL Data Area 또는 SQLVAR 라는 특수 데이터 구조를 통해 문에 대 한 매개 변수 값을 전달 합니다.  
  
3.  프로그램은 동적 문이 실행 될 때마다 다른 매개 변수 값을 제공 하 여 EXECUTE 문을 반복적으로 사용할 수 있습니다.  
  
 준비 된 실행은 여전히 정적 SQL과 동일 하지 않습니다. 정적 SQL에서 SQL 문을 처리 하는 처음 네 단계는 컴파일 타임에 발생 합니다. 준비 된 실행에서는 이러한 단계가 런타임에 발생 하지만 한 번만 수행 됩니다. 실행을 호출 하는 경우에만 계획 실행이 수행 됩니다. 이렇게 하면 동적 SQL의 아키텍처에 내재 된 성능상의 단점을 제거 하는 데 도움이 됩니다.
