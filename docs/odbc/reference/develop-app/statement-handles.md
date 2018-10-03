---
title: 문 핸들 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0be194c8e730f1ef797d0db30ff9942735f51617
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618901"
---
# <a name="statement-handles"></a>명령문 핸들
A *문* 은 가장 쉽게 생각할 SQL 문 처럼 같은 **선택 \* 에서 직원**합니다. 그러나 문이 지 이상의 SQL 문을-예:는 문에 의해 생성 된 결과 집합 및 매개 변수는 문 실행에 사용 되는 해당 SQL 문과 사용 하 여 연결 정보를 모두의 구성 됩니다. 문을 필요가 없습니다 SQL 문이 응용 프로그램 정의 합니다. 예를 들어 경우 카탈로그 함수가 같은 **SQLTables** 실행 되는 문의 테이블 이름 목록을 반환 하는 미리 정의 된 SQL 문을 실행 합니다.  
  
 각 문은 문 핸들에 의해 식별 됩니다. 문을 단일 연결을 사용 하 여 연결 되며 해당 연결에서 여러 문이 있을 수 있습니다. 일부 드라이버 지; 활성 문 수를 제한 합니다. 옵션은 SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo** 얼마나 많은 활성 문을 단일 연결에서 지 원하는 드라이버를 지정 합니다. 문을 다음과 같이 정의 됩니다 *active* 보류 중인 결과가 있으면 여기서 결과 결과 집합 또는 영향을 받는 행의 수는 **삽입**합니다 **업데이트**, 또는 **삭제할** 문 또는 데이터에 대 한 여러 호출을 사용 하 여 전송 중인 **SQLPutData**합니다.  
  
 문 핸들 ODBC (드라이버 관리자 또는 드라이버)를 구현 하는 코드 부분 내에서 같은 문 정보를 포함 하는 구조체를 식별 합니다.  
  
-   설명의 상태  
  
-   현재 문 수준 진단  
  
-   응용 프로그램 변수의 주소를 문의 매개 변수에 바인딩할 및 결과 집합 열의  
  
-   각 문 특성의 현재 설정  
  
 문 핸들은 대부분의 ODBC 함수에 사용 됩니다. 특히 사용할 함수에서를 매개 변수 바인딩 및 결과 집합 열의 (**SQLBindParameter** 하 고 **SQLBindCol**), 준비 및 문 실행 (**SQLPrepare** 를 **SQLExecute**, 및 **SQLExecDirect**), 메타 데이터 검색 (**SQLColAttribute** 및 **SQLDescribeCol**), fetch 결과 (**SQLFetch**), 진단 검색 및 (**SQLGetDiagField** 하 고 **SQLGetDiagRec**). 카탈로그 함수에도 사용 됩니다 (**SQLColumns**를 **SQLTables**등) 및 여러 다른 기능입니다.  
  
 사용 하 여 문 핸들 할당 됩니다 **SQLAllocHandle** 및 사용 하 여 해제 된 **SQLFreeHandle**합니다.
