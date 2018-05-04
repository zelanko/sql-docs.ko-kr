---
title: '4a 단계: 결과 인출 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d8d2e5bd80e47db5a5e3484aebfe2bf1d6fff9a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="step-4a-fetch-the-results"></a>4a 단계: 결과 인출 합니다.
다음 그림에 나와 있는 것 처럼 결과 인출 하는 다음 단계가입니다.  
  
 ![ODBC 응용 프로그램에서 결과 페치하](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 "단계 3:: 빌드 및 실행 된 SQL 문"에서 실행 된 문의 경우 한 **선택** 응용 프로그램 먼저 호출 문 또는 카탈로그 함수 **SQLNumResultCols** 열 번호를 확인 하려면 결과 집합입니다. 이 단계는 응용 프로그램이 이미 SQL 문의 경우 세로 또는 사용자 지정 응용 프로그램에 하드 코드 등의 열 집합 결과의 수를 알고 있는 경우에 필요는 없습니다.  
  
 응용 프로그램 이름, 데이터 형식, 정밀도 및와 각 결과 집합 열의 소수 자릿수를 검색 하는 다음으로, **SQLDescribeCol**합니다. 다시이 정보를 이미 알고 있는 세로 및 사용자 지정 응용 프로그램과 같은 응용 프로그램 필요 하지 않습니다. 응용 프로그램에는이 정보를 전달 **SQLBindCol**, 결과 집합의 열을 바인딩하는 응용 프로그램 변수입니다.  
  
 응용 프로그램 지금 호출 **SQLFetch** 데이터의 첫 번째 행을 검색 하 고로 바인딩된 변수에 해당 행에서 데이터를 **SQLBindCol**합니다. 그런 다음 호출 하는 행에 긴 데이터 있으면 **SQLGetData** 해당 데이터를 검색 합니다. 호출 응용 프로그램이 계속 **SQLFetch** 및 **SQLGetData** 추가 데이터를 검색 합니다. 데이터 페치를 완료 한 후 호출 **SQLCloseCursor** 를 커서를 닫습니다.  
  
 결과 검색 하는 자세한 내용은 참조 하십시오. [검색 결과 (기본)](../../../odbc/reference/develop-app/retrieving-results-basic.md) 및 [검색 결과 (고급)](../../../odbc/reference/develop-app/retrieving-results-advanced.md)합니다.  
  
 응용 프로그램을 지금 "단계 3:: 빌드 및 실행 된 SQL 문에" 동일한 트랜잭션에서 다른 문을 실행할 수 반환 또는 "단계 5:: Commit Transaction" 커밋하거나 트랜잭션을로 진행 합니다.
