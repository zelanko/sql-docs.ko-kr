---
title: "상대 및 절대 스크롤 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32782c2fe59aaf36fa8741870a798163d923a3a1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="relative-and-absolute-scrolling"></a>상대 및 절대 스크롤
대부분의 스크롤 옵션의 **SQLFetchScroll** 현재 위치를 기준으로 또는 절대 위치에 커서를 놓습니다. **SQLFetchScroll** 다음 인출 지원 이전, 첫 번째 및 마지막 행 집합으로도 같이 상대 인출 (행 집합을 인출할  *n*  현재 행 집합의 시작 부분부터 행)과 절대 인출 (fetch는 행에서 시작 하는 행 집합  *n* ). 경우  *n*  는 절대 인출에서 음수 이면 행 결과 집합의 끝에서 계산 됩니다. 따라서 결과 집합의 마지막 행으로 시작 하는 행 집합을 인출 하는 – 1 행의 절대 인출을 의미 합니다.  
  
 동적 커서에 삽입 하 고이 느려질 수는 결과 집합의 시작 부분부터 읽기 이외의 특정 숫자에서 행을 검색 하는 동적 커서에 대 한 쉬운 방법이 있으면 되므로 결과 집합에서 삭제 된 행을 검색 합니다. 또한, 절대 인출은 그다지 유용 하지 동적 커서에서 행을 삽입 / 삭제 행 번호 변경 때문에 따라서 연속적으로 동일한 행 수를 가져오는 다른 행 양도할 수 있습니다.  
  
 사용 하는 응용 프로그램 **SQLFetchScroll** 해당 블록에 대 한 보고서와 같이 커서 기능 가능성이 결과 집합을 한 번 통과 옵션을 사용 하 여 다음 행 집합을 인출 하 합니다. 화면 기반 응용 프로그램, 반면에 활용할 수의 모든 기능 **SQLFetchScroll**합니다. 스크롤 막대 작업에 대 한 호출에 직접 변환할 수 있으며이 경우 응용 프로그램이 화면에 표시 되는 행의 수는 행 집합 크기를 설정 하 고 화면 버퍼를 결과 집합에 바인딩합니다를 **SQLFetchScroll**합니다.  
  
|스크롤 막대 작업|SQLFetchScroll 스크롤 옵션|  
|--------------------------|-------------------------------------|  
|페이지 위로|SQL_FETCH_PRIOR|  
|페이지 아래로|SQL_FETCH_NEXT|  
|줄 위로|인 SQL_FETCH_RELATIVE *FetchOffset* -1과 같음|  
|줄 아래로|인 SQL_FETCH_RELATIVE *FetchOffset* 1|  
|스크롤 상자 위쪽에|SQL_FETCH_FIRST|  
|스크롤 상자 맨 아래에|SQL_FETCH_LAST|  
|임의 스크롤 상자 위치|SQL_FETCH_ABSOLUTE|  
  
 또한 이러한 응용 프로그램에서는 현재 행 번호와 행 수가 필요한 스크롤 작업 후 스크롤 상자 위치를 지정 해야 합니다. 현재 행 번호에 대 한 응용 프로그램 하거나의 추적할 수는 현재 행 번호 또는 호출 **SQLGetStmtAttr** 검색할 SQL_ATTR_ROW_NUMBER 특성을 사용 합니다.  
  
 커서는 결과의 크기를의 행 수 설정, 진단 헤더의 SQL_DIAG_CURSOR_ROW_COUNT 필드로 제공 됩니다. 이 필드의 값은 정의 된 후에 **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResult** 가 호출 되었습니다. 이 개수는 대략적인 개수 또는 드라이버의 기능에 따라 정확한 개수 될 수 있습니다. 드라이버의 지원을 호출 하 여 확인할 수 있습니다 **SQLGetInfo** 커서 특성 정보 유형 및 SQL_CA2_CRC_APPROXIMATE 또는 SQL_CA2_CRC_EXACT 비트 커서의 종류에 반환 되는지 여부를 확인 합니다.  
  
 정확한 행 수는 동적 커서에 대해 지원 되지 않습니다. 다른 유형의 커서에 대 한 드라이버 중 정확한 수 또는 대략적인 행 개수를 하나만 지원할 수 있습니다. 정확한 아니고 대략적인 드라이버가 지 원하는 특정 커서 유형에 대해 행 개수, SQL_DIAG_CURSOR_ROW_COUNT 필드 지금까지 인출 된 행 수를 포함 합니다. 어떤 드라이버 지원에 관계 없이 **SQLFetchScroll** 와 *작업* SQL_FETCH_LAST의 정확한 행 수를 포함 하도록 SQL_DIAG_CURSOR_ROW_COUNT 필드 발생 합니다.
