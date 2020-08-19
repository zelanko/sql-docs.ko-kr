---
description: 상대 및 절대 스크롤
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c7471e7ee245d9cf70adc8c3453705453bc1aac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482946"
---
# <a name="relative-and-absolute-scrolling"></a>상대 및 절대 스크롤
**Sqlfetchscroll** 의 스크롤 옵션 대부분은 커서를 현재 위치를 기준으로 또는 절대 위치에 상대적으로 배치 합니다. **Sqlfetchscroll** 은 다음, 이전, 첫 번째 및 마지막 행 집합을 인출 하 고, 상대 인출 (현재 행 집합의 시작 부분에서 행 집합 *n* 행 인출) 및 절대 인출 (행 *n*에서 시작 하 여 행 집합 인출)을 지원 합니다. 절대 인출에서 *n* 이 음수 이면 결과 집합의 끝에서 행이 계산 됩니다. 즉,-1 행의 절대 페치는 결과 집합의 마지막 행으로 시작 하는 행 집합을 인출 하는 것을 의미 합니다.  
  
 동적 커서는 결과 집합에서 삽입 및 삭제 된 행을 감지 하므로 동적 커서는 결과 집합의 시작 부분에서 읽는 것이 아닌 특정 수의 행을 검색 하는 쉬운 방법이 없으므로 속도가 느릴 수 있습니다. 또한 행이 삽입 되 고 삭제 되 면 행 번호가 변경 되기 때문에 동적 커서에는 절대 페치가 그다지 유용 하지 않습니다. 따라서 동일한 행 번호를 연속적으로 가져오면 다른 행이 생성 될 수 있습니다.  
  
 보고서와 같은 블록 커서 기능에 대해서만 **Sqlfetchscroll** 을 사용 하는 응용 프로그램은 다음 행 집합을 인출 하는 옵션만 사용 하 여 결과 집합을 한 번에 전달할 수 있습니다. 반면에 화면 기반 응용 프로그램은 **Sqlfetchscroll**의 모든 기능을 활용할 수 있습니다. 응용 프로그램에서 행 집합 크기를 화면에 표시 되는 행 수로 설정 하 고 화면 버퍼를 결과 집합에 바인딩하는 경우 스크롤 막대 작업을 **Sqlfetchscroll**에 대 한 호출로 직접 변환할 수 있습니다.  
  
|스크롤 막대 작업|SQLFetchScroll 스크롤 옵션|  
|--------------------------|-------------------------------------|  
|페이지 위로|SQL_FETCH_PRIOR|  
|페이지 아래로|SQL_FETCH_NEXT|  
|줄 위로|*Fetchoffset* 이-1과 같은 SQL_FETCH_RELATIVE|  
|줄 아래로|*Fetchoffset* 이 1과 같은 SQL_FETCH_RELATIVE|  
|위쪽의 스크롤 상자|SQL_FETCH_FIRST|  
|아래쪽의 스크롤 상자|SQL_FETCH_LAST|  
|임의 스크롤 상자 위치|SQL_FETCH_ABSOLUTE|  
  
 또한 이러한 응용 프로그램은 스크롤 작업 후에 스크롤 상자를 배치 해야 합니다 .이 경우에는 현재 행 번호와 행 수가 필요 합니다. 현재 행 번호의 경우 응용 프로그램은 현재 행 번호를 추적 하거나 SQL_ATTR_ROW_NUMBER 특성을 사용 하 여 **SQLGetStmtAttr** 를 호출 하 여 검색할 수 있습니다.  
  
 결과 집합의 크기에 해당 하는 커서의 행 수는 진단 헤더의 SQL_DIAG_CURSOR_ROW_COUNT 필드로 사용할 수 있습니다. 이 필드의 값은 **Sqlexecute**, **Sqlexecdirect**또는 **SQLMoreResult** 가 호출 된 후에만 정의 됩니다. 이 개수는 대략적인 개수 또는 정확한 카운트 중에서 드라이버의 기능에 따라 달라질 수 있습니다. 커서 특성 정보 형식으로 **SQLGetInfo** 를 호출 하 고 커서 유형에 대해 SQL_CA2_CRC_APPROXIMATE 또는 SQL_CA2_CRC_EXACT 비트가 반환 되는지 확인 하 여 드라이버의 지원을 확인할 수 있습니다.  
  
 동적 커서에 대해 정확한 행 수가 지원 되지 않습니다. 다른 유형의 커서의 경우 드라이버는 정확히 또는 대략적인 행 개수 중 하나만 지원할 수 있습니다. 드라이버가 특정 커서 유형에 대 한 정확한 행 개수와 대략적인 행 수를 모두 지원 하지 않는 경우 SQL_DIAG_CURSOR_ROW_COUNT 필드에는 지금까지 인출 된 행의 수가 포함 됩니다. 드라이버가 지 원하는 항목에 관계 없이 **Sqlfetchscroll** SQL_FETCH_LAST *작업* 을 사용 하면 SQL_DIAG_CURSOR_ROW_COUNT 필드에 정확한 행 개수가 포함 됩니다.
