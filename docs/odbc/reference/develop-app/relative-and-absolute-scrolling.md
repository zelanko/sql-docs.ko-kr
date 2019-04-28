---
title: 상대 및 절대 스크롤 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ba05cb9079514750cf087149bae476efe0d8d41
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861513"
---
# <a name="relative-and-absolute-scrolling"></a>상대 및 절대 스크롤
스크롤 옵션의 대부분 **SQLFetchScroll** 현재 위치를 기준으로 또는 절대 위치에 커서를 놓습니다. **SQLFetchScroll** 다음을 인출할 이전, 첫 번째 및 마지막 행 집합에도으로 상대 인출로 (행 집합을 인출할 *n* 현재 행 집합의 시작 부분에서 행)과 절대 인출 (페치를 시작 하는 행 집합 행 *n*). 하는 경우 *n* 는 절대 인출에서 음수 이면 행 결과 집합의 끝에서 계산 됩니다. 따라서 결과 집합의 마지막 행을 시작 하는 행 집합을 인출 하는-1 행의 절대 인출을 의미 합니다.  
  
 동적 커서는 삽입 및 느린 나올 수 있는 결과 집합의 시작 부분에서 읽기 이외의 특정 수의 행을 검색 하는 동적 커서에 대 한 쉬운 방법이 있으면 되므로 결과 집합에서 삭제 된 행을 검색 합니다. 또한, 절대 인출 그다지 유용 하지 동적 커서에서 행을 삭제와 삽입은 행 번호가 변경 되므로 따라서 동일한 행 수를 가져오는 연속 해 서 다른 행을 얻을 수 있습니다.  
  
 사용 하는 응용 프로그램 **SQLFetchScroll** 해당 블록에 대해서만 보고서와 같은 커서 기능 가능성이 결과 집합을 한 번 통과 옵션만 사용 하 여 다음 행 집합을 가져올 수 있습니다. 화면 기반 응용 프로그램, 다른 한편으로 활용할 수의 모든 기능 **SQLFetchScroll**합니다. 응용 프로그램 화면에 표시 되는 행의 수는 행 집합 크기를 설정 하 고 화면 버퍼를 결과 집합에 바인딩합니다를 경우 스크롤 막대 작업에 대 한 호출을 직접 변환할 수 있습니다 **SQLFetchScroll**합니다.  
  
|스크롤 막대 작업|SQLFetchScroll 스크롤 옵션|  
|--------------------------|-------------------------------------|  
|페이지 위로|SQL_FETCH_PRIOR|  
|페이지 아래로|SQL_FETCH_NEXT|  
|줄 위로|인 SQL_FETCH_RELATIVE *FetchOffset* -1|  
|줄 아래로|인 SQL_FETCH_RELATIVE *FetchOffset* 1|  
|맨 위에 있는 스크롤 상자|SQL_FETCH_FIRST|  
|스크롤 상자 맨 아래에 있는|SQL_FETCH_LAST|  
|임의 스크롤 상자 위치|SQL_FETCH_ABSOLUTE|  
  
 또한 이러한 응용 프로그램 현재 행 번호 및 행 수를 필요한 스크롤 작업 후 스크롤 상자를 배치 해야 합니다. 현재 행 번호에 대 한 응용 프로그램 중 하나를 추적할 수는 현재 행 번호 또는 통화 **SQLGetStmtAttr** 키 값을 검색할 SQL_ATTR_ROW_NUMBER 특성을 사용 합니다.  
  
 결과의 크기는 커서의 행 수 설정, 진단 헤더의 SQL_DIAG_CURSOR_ROW_COUNT 필드로 사용할 수 있습니다. 이 필드의 값을 설정한 후에 정의 됩니다 **SQLExecute**를 **SQLExecDirect**, 또는 **SQLMoreResult** 가 호출 되었습니다. 이 개수는 대략적인 개수 또는 드라이버의 기능에 따라 정확한 개수를 수 있습니다. 드라이버의 지원을 호출 하 여 확인할 수 있습니다 **SQLGetInfo** 커서 특성 정보 유형 및 커서 유형에 대해 SQL_CA2_CRC_APPROXIMATE 또는 SQL_CA2_CRC_EXACT 비트가 반환 되는지 여부를 확인 합니다.  
  
 동적 커서에 대 한 정확한 행 수를 지원 하지 않습니다. 다른 유형의 커서에 대 한 드라이버는 정확 하거나 대략적인 행 개수, 하지만 둘 다를 지원할 수 있습니다. 정확한 아니고 대략적인 드라이버에서 지 원하는 경우 특정 커서 유형에 대해 행 개수, SQL_DIAG_CURSOR_ROW_COUNT 필드는 지금까지 인출 된 행의 수를 포함 합니다. 어떤 드라이버 지원에 관계 없이 **SQLFetchScroll** 사용 하 여는 *작업* SQL_FETCH_LAST의 정확한 행 수를 포함 하도록 SQL_DIAG_CURSOR_ROW_COUNT 필드 발생 합니다.
