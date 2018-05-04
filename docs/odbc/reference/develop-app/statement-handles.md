---
title: 문 핸들 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bd4d07e87af049ac59bc63faf119e84872bbc45
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="statement-handles"></a>문 핸들
A *문을* 은 가장 쉽게 생각할 SQL 문 처럼 같은 **선택 \* 에서 직원**합니다. 그러나 문을 SQL 문을 보다 더-예: 문에 의해 만들어진 결과 집합 및 매개 변수는 문 실행에 사용 되는 해당 SQL 문이와 관련 된 정보를 모두 이루어져 있습니다. 문을 하지 않아도 응용 프로그램 정의 된 SQL 문이 있습니다. 예를 들어 때 카탈로그 함수가 같은 **SQLTables** 실행 되는 테이블 이름 목록을 반환 하는 미리 정의 된 SQL 문을 실행 하는 문에서 합니다.  
  
 각 문에 문 핸들에 의해 식별 됩니다. 문을 단일 연결에 연결 되며 해당 연결에서 여러 문이 있을 수 있습니다. 일부 드라이버 지 원하는; 활성 문 수를 제한 합니다. 옵션에 SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo** 단일 연결에는 드라이버에서 지 원하는 활성 문 수를 지정 합니다. 문이 정의 됩니다. *활성* 보류 중인 결과가 있으면 여기서 결과 결과 집합 또는 영향을 받는 행의 수는 **삽입**, **업데이트**, 또는 **삭제** 문 또는 데이터를 여러 번 호출 함께 전송 되는 **SQLPutData**합니다.  
  
 문 핸들의 ODBC (드라이버 관리자 또는 드라이버)를 구현 하는 코드 조각 내에서 같은 문 정보를 포함 하는 구조를 식별 합니다.  
  
-   설명의 상태  
  
-   현재 문 수준 진단  
  
-   응용 프로그램 변수의 주소는 문의 매개 변수에 바인딩할 및 결과 집합 열의  
  
-   각 문 특성의 현재 설정  
  
 문 핸들은 대부분의 ODBC 함수에 사용 됩니다. 특히, 사용 되는 함수에 매개 변수 바인딩 및 결과 집합 열의 (**SQLBindParameter** 및 **SQLBindCol**), 준비 하 고 문 실행 (**SQLPrepare** **SQLExecute**, 및 **SQLExecDirect**), 메타 데이터 검색 (**SQLColAttribute** 및 **SQLDescribeCol**), fetch 결과 (**SQLFetch**), 진단을 검색할 및 (**SQLGetDiagField** 및 **SQLGetDiagRec**). 카탈로그 함수에도 사용 됩니다 (**SQLColumns**, **SQLTables**등) 및 여러 다른 함수가 있습니다.  
  
 사용 하 여 문 핸들 할당은 **SQLAllocHandle** 로 해제 및 **SQLFreeHandle**합니다.
