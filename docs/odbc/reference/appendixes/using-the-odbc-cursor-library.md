---
title: ODBC 커서 라이브러리 사용 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c740ed78de51684eac38ad0c54ab2224986018d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301404"
---
# <a name="using-the-odbc-cursor-library"></a>ODBC 커서 라이브러리 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 ODBC 커서 라이브러리를 사용하려면 응용 프로그램을 사용합니다.  
  
1.  **SQLSetConnectAttr을** SQL_ATTR_ODBC_CURSORS *특성을* 사용하여 커서 라이브러리를 특정 연결에서 사용하는 방법을 지정합니다. 커서 라이브러리는 항상 사용할 수 있습니다(SQL_CUR_USE_ODBC), 드라이버가 스크롤 가능한 커서(SQL_CUR_USE_IF_NEEDED)를 지원하지 않거나 사용되지 않는 경우에만 사용(SQL_CUR_USE_DRIVER).  
  
2.  데이터 원본에 연결하려면 **SQLConnect,** **SQLDriverConnect**또는 **SQLBrowseConnect를** 호출합니다.  
  
3.  **SQLSetStmtAttr을** 호출하여 커서 유형(SQL_ATTR_CURSOR_TYPE), 동시성(SQL_ATTR_CONCURRENCY) 및 행 집합 크기(SQL_ATTR_ROW_ARRAY_SIZE)를 지정합니다. 커서 라이브러리는 정방향 전용 및 정적 커서를 지원합니다. 정방향 전용 커서는 읽기 전용이어야 하며 정적 커서는 읽기 전용이거나 값을 비교하는 낙관적 동시성 컨트롤을 사용할 수 있습니다.  
  
4.  하나 이상의 행 집합 버퍼를 할당하고 **SQLBindCol을** 하나 이상 호출하여 이러한 버퍼를 연수하여 설정 열을 생성합니다.  
  
5.  **SELECT** 문 또는 프로시저를 실행하거나 카탈로그 함수를 호출하여 결과 집합을 생성합니다. 응용 프로그램이 위치 가 있는 업데이트 문을 실행하는 경우 **UPDATE FOR SELECT** 문을 실행하여 결과 집합을 생성해야 합니다.  
  
6.  결과 집합을 스크롤하려면 **SQLFetch** 또는 **SQLFetch스크롤을** 하나 이상 호출합니다.  
  
 응용 프로그램은 행 집합 버퍼의 데이터 값을 변경할 수 있습니다. 커서 라이브러리의 캐시에서 데이터로 행 집합 버퍼를 새로 고치려면 응용 프로그램이 *fetchOrientation* 인수를 SQL_FETCH_RELATIVE 설정하고 *FetchOffset* 인수를 0으로 설정한 **SQLFetchScroll를** 호출합니다.  
  
 언바운드 열에서 데이터를 검색하기 위해 응용 프로그램은 **SQLSetPos를** 호출하여 원하는 행에 커서를 배치합니다. 그런 다음 **SQLGetData를** 호출하여 데이터를 검색합니다.  
  
 데이터 원본에서 검색된 행 수를 확인하려면 응용 프로그램에서 **SQLRowCount**를 호출합니다.
