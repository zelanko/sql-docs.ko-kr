---
title: '4a단계: 결과 가져올 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cad33f1ccf798a08ef1f11667e59b4d5fb4888d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149207"
---
# <a name="step-4a-fetch-the-results"></a>4a단계: 결과 페치
다음 그림에 나와 있는 것 처럼 결과 인출 하는 다음 단계가입니다.  
  
 ![ODBC 응용 프로그램에서 결과 페치하](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 문을 실행 하는 경우 "3 단계: "빌드하고 SQL 문을 실행 했습니다를 **선택** 응용 프로그램은 먼저 호출 문 또는 카탈로그 함수 **SQLNumResultCols** 결과 집합의 열 수를 결정 합니다. 이 단계가 응용 프로그램이 이미 SQL 문의 경우 처럼 세로 또는 사용자 지정 응용 프로그램에서 하드 코드 된 열 집합 결과의 수를 아는 경우에 필요 하지 않습니다.  
  
 응용 프로그램 이름, 데이터 형식, 전체 자릿수 및 사용 하 여 각 결과 집합 열의 소수 자릿수를 검색 하는 어 **SQLDescribeCol**합니다. 마찬가지로이 정보를 이미 알고 있는 세로 및 사용자 지정 응용 프로그램과 같은 응용 프로그램에 필요한 아닙니다. 응용 프로그램에는이 정보를 전달 **SQLBindCol**, 결과 집합의 열에 대 한 응용 프로그램 변수에 바인딩하는 합니다.  
  
 응용 프로그램이 이제 호출 **SQLFetch** 데이터의 첫 번째 행을 가져와 바인딩된 변수에서 해당 행에서 데이터를 배치할 **SQLBindCol**합니다. 그런 다음 호출 행에 long 데이터가 있으면 **SQLGetData** 해당 데이터를 검색 합니다. 호출 응용 프로그램을 계속 **SQLFetch** 하 고 **SQLGetData** 추가 데이터를 검색 합니다. 데이터를 가져오는 중, 완료 된 후 호출 **SQLCloseCursor** 를 커서를 닫습니다.  
  
 결과 검색 하는 설명은 참조 하세요 [검색 결과 (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md) 하 고 [검색 결과 (고급)](../../../odbc/reference/develop-app/retrieving-results-advanced.md)합니다.  
  
 이제 응용 프로그램에 반환 합니다. "3 단계: 빌드 및 SQL 문을 실행할 "는 동일한 트랜잭션에서 다른 문을 실행 하려면 진행 또는 "5 단계: 트랜잭션 커밋"커밋 또는 트랜잭션을 롤백합니다.
