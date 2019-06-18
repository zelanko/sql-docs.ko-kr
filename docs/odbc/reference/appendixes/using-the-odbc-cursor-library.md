---
title: ODBC 커서 라이브러리를 사용 하 여 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9fe19efb2d39e875cdafec76f2c50164f3a66f03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735028"
---
# <a name="using-the-odbc-cursor-library"></a>ODBC 커서 라이브러리 사용
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 에 ODBC 커서 라이브러리를 응용 프로그램을 사용 합니다.  
  
1.  호출 **SQLSetConnectAttr** 사용 하 여는 *특성* 의 SQL_ATTR_ODBC_CURSORS 어떻게 특정 연결을 사용 하 여 커서 라이브러리를 사용 해야 할지 지정 합니다. 커서 라이브러리는 항상 수 (SQL_CUR_USE_ODBC) 사용, 드라이버는 스크롤 가능한 커서 (SQL_CUR_USE_IF_NEEDED)를 지원 하지 않는 경우에 사용 되는 또는 (SQL_CUR_USE_DRIVER) 사용 되지 않습니다.  
  
2.  호출 **SQLConnect**를 **SQLDriverConnect**, 또는 **SQLBrowseConnect** 데이터 원본에 연결 합니다.  
  
3.  호출 **SQLSetStmtAttr** 커서 유형 (SQL_ATTR_CURSOR_TYPE), (SQL_ATTR_CONCURRENCY) 동시성 및 행 집합 크기 (SQL_ATTR_ROW_ARRAY_SIZE)를 지정 합니다. 커서 라이브러리는 정방향 전용 및 정적 커서를 지원합니다. 정적 커서는 읽기 전용 수 또는 값을 비교 하는 낙관적 동시성 제어를 사용할 수 있지만 정방향 전용 커서는 읽기 전용 이어야 합니다.  
  
4.  하나 이상의 행 집합 버퍼 및 호출 할당 **SQLBindCol** 한 번 이상 나타나는 결과 집합 열의 이러한 버퍼를 바인딩합니다.  
  
5.  결과 실행 하 여 집합을 생성 한 **선택** 문 또는 프로시저를 카탈로그 함수를 호출 하 여. 실행 하는 응용 프로그램이 위치 지정된 update 문을 실행 하는 경우는 **업데이트에 대 한 선택** 문의 결과 집합을 생성 합니다.  
  
6.  호출 **SQLFetch** 하거나 **SQLFetchScroll** 한 번 이상 나타나는 결과 집합을 스크롤할 수 있습니다.  
  
 응용 프로그램 버퍼 행 집합의에서 데이터 값을 변경할 수 있습니다. 응용 프로그램이 호출 커서 라이브러리 캐시에서 데이터를 사용 하 여 행 집합 버퍼를 새로 고치려면 **SQLFetchScroll** 사용 하 여 합니다 *FetchOrientation* 인수와 함께 SQL_FETCH_RELATIVE 및 *FetchOffset* 인수는 0으로 설정 합니다.  
  
 바인딩되지 않은 열을 호출 하 여 응용 프로그램에서 데이터를 검색할 **SQLSetPos** 원하는 행에 커서를 배치 합니다. 그런 다음 호출 **SQLGetData** 데이터를 검색 합니다.  
  
 데이터 원본에서 검색 된 행 수를 확인 하려면 응용 프로그램 호출 **SQLRowCount**합니다.
