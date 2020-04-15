---
title: '4a 단계: 결과 가져오기 | 마이크로 소프트 문서'
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
ms.openlocfilehash: c4f810e5c42b54ec871c233ab498936abae610dc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302974"
---
# <a name="step-4a-fetch-the-results"></a>4a단계: 결과 페치
다음 단계는 다음 그림과 같이 결과를 가져오는 것입니다.  
  
 ![ODBC 응용 프로그램에서 결과를 페치하는 방법](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 "3단계: SQL 문 빌드 및 실행"에서 실행된 명령문이 **SELECT** 문 또는 카탈로그 함수인 경우 응용 프로그램은 먼저 **SQLNumResultCols를** 호출하여 결과 집합의 열 수를 결정합니다. SQL 문이 세로 또는 사용자 지정 응용 프로그램에서 하드 코딩되는 경우와 같이 응용 프로그램에서 결과 집합 열의 수를 이미 알고 있는 경우에는 이 단계가 필요하지 않습니다.  
  
 다음으로 응용 프로그램은 **SQLDescribeCol을**사용하여 각 결과 집합 열의 이름, 데이터 형식, 정밀도 및 배율을 검색합니다. 이 정보를 이미 알고 있는 수직 및 사용자 지정 응용 프로그램과 같은 응용 프로그램에는 이 정보가 필요하지 않습니다. 응용 프로그램은 이 정보를 **SQLBindCol에**전달하여 결과 집합의 열에 응용 프로그램 변수를 바인딩합니다.  
  
 이제 응용 프로그램은 **SQLFetch를** 호출하여 데이터의 첫 번째 행을 검색하고 **SQLBindCol로**바인딩된 변수에 해당 행의 데이터를 배치합니다. 행에 긴 데이터가 있으면 **SQLGetData를** 호출하여 해당 데이터를 검색합니다. 응용 프로그램은 추가 데이터를 검색하기 위해 **SQLFetch** 및 **SQLGetData를** 계속 호출합니다. 데이터 가져오기가 완료되면 **SQLCloseCursor를** 호출하여 커서를 닫습니다.  
  
 결과 검색에 대한 전체 설명은 [결과 검색(기본)](../../../odbc/reference/develop-app/retrieving-results-basic.md) 및 [결과 검색(고급)을](../../../odbc/reference/develop-app/retrieving-results-advanced.md)참조하십시오.  
  
 이제 응용 프로그램이 "3단계: SQL 문을 빌드하고 실행"으로 돌아와 동일한 트랜잭션에서 다른 문을 실행합니다. 또는 "5단계: 트랜잭션 커밋"으로 진행하여 트랜잭션을 커밋하거나 롤백합니다.
