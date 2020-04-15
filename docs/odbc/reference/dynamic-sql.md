---
title: 동적 SQL | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56419723540114f122be2582f0de7c7e7d0c54f3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306691"
---
# <a name="dynamic-sql"></a>동적 SQL
정적 SQL은 많은 상황에서 잘 작동하지만 데이터 액세스를 미리 확인할 수 없는 응용 프로그램 클래스가 있습니다. 예를 들어, 스프레드시트를 통해 사용자가 쿼리를 입력할 수 있다고 가정하고, 이 쿼리는 스프레드시트가 DBMS로 전송하여 데이터를 검색합니다. 스프레드시트 프로그램을 작성할 때 이 쿼리의 내용은 프로그래머에게 알 수 없습니다.  
  
 이 문제를 해결하기 위해 스프레드시트는 동적 SQL이라는 임베디드 SQL의 형태를 사용합니다. 프로그램에서 하드 코딩된 정적 SQL 문과 달리 동적 SQL 문은 런타임에 빌드하고 문자열 호스트 변수에 배치할 수 있습니다. 그런 다음 처리를 위해 DBMS로 전송됩니다. DBMS는 동적 SQL 문을 위해 런타임에 액세스 계획을 생성해야 하므로 동적 SQL은 일반적으로 정적 SQL보다 느립니다. 동적 SQL 문을 포함하는 프로그램이 컴파일되면 정적 SQL과 마찬가지로 동적 SQL 문이 프로그램에서 제거되지 않습니다. 대신 문을 DBMS에 전달하는 함수 호출로 대체됩니다. 동일한 프로그램의 정적 SQL 문은 정상적으로 처리됩니다.  
  
 동적 SQL 문을 실행하는 가장 간단한 방법은 EXECUTE 즉시 문을 사용하면 됩니다. 이 문은 컴파일 및 실행을 위해 SQL 문을 DBMS에 전달합니다.  
  
 EXECUTE 즉시 문의 한 가지 단점은 DBMS문이 실행될 때마다 SQL 문을 처리하는 다섯 단계 각각을 거쳐야 한다는 것입니다. 많은 문이 동적으로 실행되는 경우 이 프로세스와 관련된 오버헤드가 중요할 수 있으며 이러한 문이 유사한 경우 낭비됩니다. 이러한 상황을 해결하기 위해 동적 SQL은 준비된 실행이라는 최적화된 실행 형식을 제공하며, 다음 단계를 사용합니다.  
  
1.  프로그램은 EXECUTE 즉시 문과 마찬가지로 버퍼에서 SQL 문을 생성합니다. 호스트 변수 대신 물음표(?)를 문 텍스트의 아무 곳이나 상수로 대체하여 상수값이 나중에 제공될 것임을 나타낼 수 있습니다. 물음표는 매개 변수 마커라고 합니다.  
  
2.  프로그램은 SQL 문을 준비 문으로 DBMS에 전달하여 DBMS가 문을 구문 분석, 유효성 검사 및 최적화하고 실행 계획을 생성하도록 요청합니다. 그런 다음 프로그램은 EXECUTE 문(EXECUTE 즉시 문이 아님)을 사용하여 나중에 PREPARE 문을 실행합니다. SQL 데이터 영역 또는 SQLDA라는 특수 데이터 구조를 통해 문의 매개 변수 값을 전달합니다.  
  
3.  프로그램은 EXECUTE 문을 반복적으로 사용하여 동적 문이 실행될 때마다 다른 매개 변수 값을 제공할 수 있습니다.  
  
 준비된 실행은 여전히 정적 SQL과 동일하지 않습니다. 정적 SQL에서 SQL 문을 처리하는 처음 네 단계는 컴파일 타임에 수행됩니다. 준비된 실행에서는 이러한 단계가 런타임에 계속 수행되지만 한 번만 수행됩니다. 계획의 실행은 EXECUTE가 호출될 때만 수행됩니다. 이렇게 하면 동적 SQL 아키텍처에 내재된 몇 가지 성능 단점을 제거할 수 있습니다. 다음 그림에서는 정적 SQL, 즉각적인 실행이 있는 동적 SQL 및 준비된 실행을 가진 동적 SQL 간의 차이점을 보여 주며, 동적 SQL을 보여 주어 있습니다.
