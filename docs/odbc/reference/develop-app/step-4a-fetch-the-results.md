---
description: '4a단계: 결과 페치'
title: '4a 단계: 결과 가져오기 | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91a81809d07faafac6511bb5ec96c97d4f59d654
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491360"
---
# <a name="step-4a-fetch-the-results"></a>4a단계: 결과 페치
다음 단계는 다음 그림과 같이 결과를 인출 하는 것입니다.  
  
 ![ODBC 응용 프로그램에서 결과를 페치하는 방법](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 "3 단계: SQL 문 작성 및 실행"에서 실행 된 문이 **SELECT** 문 또는 카탈로그 함수인 경우 응용 프로그램은 먼저 **Sqlnumresultcols** 를 호출 하 여 결과 집합의 열 수를 확인 합니다. 응용 프로그램에서 SQL 문이 수직 또는 사용자 지정 응용 프로그램에 하드 코딩 된 경우와 같이 결과 집합 열의 수를 이미 알고 있는 경우에는이 단계가 필요 하지 않습니다.  
  
 그런 다음 응용 프로그램은 **SQLDescribeCol**를 사용 하 여 각 결과 집합 열의 이름, 데이터 형식, 전체 자릿수 및 소수 자릿수를 검색 합니다. 이 정보를 이미 알고 있는 수직 및 사용자 지정 응용 프로그램과 같은 응용 프로그램에는이 작업이 필요 하지 않습니다. 응용 프로그램은이 정보를 **SQLBindCol**에 전달 하 여 응용 프로그램 변수를 결과 집합의 열에 바인딩합니다.  
  
 이제 응용 프로그램은 **Sqlfetch** 를 호출 하 여 첫 번째 데이터 행을 검색 하 고 해당 행의 데이터를 **SQLBindCol**에 바인딩된 변수에 넣습니다. 행에 긴 데이터가 있으면 **SQLGetData** 를 호출 하 여 해당 데이터를 검색 합니다. 응용 프로그램은 계속 해 서 **Sqlfetch** 및 **SQLGetData** 를 호출 하 여 추가 데이터를 검색 합니다. 데이터 페치를 완료 한 후에는 **SQLCloseCursor** 를 호출 하 여 커서를 닫습니다.  
  
 결과를 검색 하는 방법에 대 한 자세한 내용은 [결과 검색 (기본)](../../../odbc/reference/develop-app/retrieving-results-basic.md) 및 [결과 검색 (고급)](../../../odbc/reference/develop-app/retrieving-results-advanced.md)을 참조 하세요.  
  
 이제 응용 프로그램이 "3 단계: SQL 문 작성 및 실행"으로 반환 되어 동일한 트랜잭션에서 다른 문을 실행 합니다. 또는 트랜잭션을 커밋하거나 롤백하려면 "5 단계: 트랜잭션 커밋"으로 진행 합니다.
