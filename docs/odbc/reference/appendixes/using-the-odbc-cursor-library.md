---
title: ODBC 커서 라이브러리 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], using cursor library
- cursor library [ODBC], using cursor library
ms.assetid: 9653f2f8-ccfc-4220-99ef-601dc0fa641c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdddf2e757c549de460f5e22c2ea76ce91a2a969
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069975"
---
# <a name="using-the-odbc-cursor-library"></a>ODBC 커서 라이브러리 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 ODBC 커서 라이브러리를 사용 하려면 다음 응용 프로그램을 사용 합니다.  
  
1.  SQL_ATTR_ODBC_CURSORS의 *특성* 을 사용 하 여 **SQLSetConnectAttr** 를 호출 하 여 특정 연결에서 커서 라이브러리를 사용 하는 방법을 지정 합니다. 커서 라이브러리는 항상 사용할 수 있습니다 (SQL_CUR_USE_ODBC). 드라이버가 스크롤 가능 커서 (SQL_CUR_USE_IF_NEEDED)를 지원 하지 않거나 사용 되지 않는 경우에만 사용 됩니다 (SQL_CUR_USE_DRIVER).  
  
2.  **SQLConnect**, **SQLDriverConnect**또는 **SQLBrowseConnect** 를 호출 하 여 데이터 원본에 연결 합니다.  
  
3.  **SQLSetStmtAttr** 를 호출 하 여 커서 유형 (SQL_ATTR_CURSOR_TYPE), 동시성 (SQL_ATTR_CONCURRENCY) 및 행 집합 크기 (SQL_ATTR_ROW_ARRAY_SIZE)를 지정 합니다. 커서 라이브러리는 앞 으로만 이동 가능한 커서를 지원 합니다. 앞 으로만 이동 가능한 커서는 읽기 전용 이거나 정적 커서는 읽기 전용 이거나 낙관적 동시성 제어를 사용 하 여 값을 비교할 수 있습니다.  
  
4.  하나 이상의 행 집합 버퍼를 할당 하 고 **SQLBindCol** 를 한 번 이상 호출 하 여 이러한 버퍼를 결과 집합 열에 바인딩합니다.  
  
5.  **SELECT** 문 또는 프로시저를 실행 하거나 카탈로그 함수를 호출 하 여 결과 집합을 생성 합니다. 응용 프로그램에서 위치 지정 update 문을 실행 하는 경우 **SELECT FOR update** 문을 실행 하 여 결과 집합을 생성 해야 합니다.  
  
6.  **Sqlfetch** 또는 **sqlfetchscroll** 을 한 번 이상 호출 하 여 결과 집합을 스크롤합니다.  
  
 응용 프로그램은 행 집합 버퍼의 데이터 값을 변경할 수 있습니다. 커서 라이브러리 캐시의 데이터로 행 집합 버퍼를 새로 고치기 위해 응용 프로그램은 *Fetchorientation* 인수를 SQL_FETCH_RELATIVE 설정 하 고 *fetchoffset* 인수를 0으로 설정 하 여 **sqlfetchscroll** 을 호출 합니다.  
  
 바인딩되지 않은 열에서 데이터를 검색 하기 위해 응용 프로그램은 **SQLSetPos** 를 호출 하 여 원하는 행에 커서를 놓습니다. 그런 다음 **SQLGetData** 를 호출 하 여 데이터를 검색 합니다.  
  
 응용 프로그램은 데이터 원본에서 검색 된 행 수를 확인 하기 위해 **Sqlrowcount**를 호출 합니다.
