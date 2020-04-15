---
title: 상대 및 절대 스크롤 | 마이크로 소프트 문서
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
ms.openlocfilehash: ae0ed5af8d116a3038b55b1e3d68231154c2a35c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300103"
---
# <a name="relative-and-absolute-scrolling"></a>상대 및 절대 스크롤
**SQLFetchScroll의** 대부분의 스크롤 옵션은 커서를 현재 위치 또는 절대 위치에 대해 배치합니다. **SQLFetchScroll는** 다음, 이전, 첫 번째 및 마지막 행 집합뿐만 아니라 상대 가져오기(현재 행 집합의 시작에서 행 집합 *n* 행을 가져오기) 및 절대 페칭(행 *n에서*시작하는 행 집합 가져오기)을 가져옵니다. 절대 가져오기에서 *n이* 음수이면 행은 결과 집합의 끝에서 계산됩니다. 따라서 행 -1의 절대 가져오기는 결과 집합의 마지막 행으로 시작하는 행 집합을 가져오는 것을 의미합니다.  
  
 동적 커서는 결과 집합에 삽입되고 삭제된 행을 감지하므로 동적 커서가 결과 집합의 시작 부분부터 읽는 것 이외에 특정 숫자로 행을 검색하는 쉬운 방법은 없습니다. 또한 행이 삽입되고 삭제될 때 행 번호가 변경되므로 절대 페칭은 동적 커서에서 별로 유용하지 않습니다. 따라서 동일한 행 번호를 연속적으로 가져오면 다른 행이 생성될 수 있습니다.  
  
 보고서와 같은 블록 커서 기능에 대해서만 **SQLFetchScroll를** 사용하는 응용 프로그램은 다음 행 집합을 가져오는 옵션만 사용하여 결과 집합을 한 번 통과할 수 있습니다. 반면에 화면 기반 응용 프로그램은 **SQLFetchScroll**의 모든 기능을 활용할 수 있습니다. 응용 프로그램이 행 집합 크기를 화면에 표시되는 행 수로 설정하고 화면 버퍼를 결과 집합에 바인딩하면 스크롤 막대 작업을 **SQLFetchScroll**에 대한 호출로 직접 변환할 수 있습니다.  
  
|스크롤 막대 작업|SQLFetchScroll 스크롤 옵션|  
|--------------------------|-------------------------------------|  
|페이지 위로|SQL_FETCH_PRIOR|  
|페이지 아래로|SQL_FETCH_NEXT|  
|줄 위로|*FetchOffset이* -1과 SQL_FETCH_RELATIVE|  
|줄 아래로|SQL_FETCH_RELATIVE *FetchOffset이* 1과 같습니다.|  
|맨 위에 있는 스크롤 상자|SQL_FETCH_FIRST|  
|하단의 스크롤 상자|SQL_FETCH_LAST|  
|임의 스크롤 상자 위치|SQL_FETCH_ABSOLUTE|  
  
 또한 이러한 응용 프로그램은 현재 행 번호와 행 수가 필요한 스크롤 작업 후에 스크롤 상자를 배치해야 합니다. 현재 행 번호의 경우 응용 프로그램은 현재 행 번호를 추적하거나 SQL_ATTR_ROW_NUMBER 특성을 사용하여 **SQLGetStmtAttr을** 호출하여 검색할 수 있습니다.  
  
 결과 집합의 크기인 커서의 행 수는 진단 헤더의 SQL_DIAG_CURSOR_ROW_COUNT 필드로 사용할 수 있습니다. 이 필드의 값은 **SQLExecute,** **SQLExecDirect**또는 **SQLMoreResult가** 호출된 후에만 정의됩니다. 이 개수는 드라이버의 기능에 따라 대략적인 개수 또는 정확한 개수일 수 있습니다. 드라이버의 지원은 cursor 특성 정보 형식을 사용 하 여 **SQLGetInfo를** 호출 하 고 SQL_CA2_CRC_APPROXIMATE 또는 SQL_CA2_CRC_EXACT 비트 커서의 형식에 대 한 반환 되는지 확인 하 여 확인할 수 있습니다.  
  
 동적 커서에 대해 정확한 행 수는 지원되지 않습니다. 다른 유형의 커서의 경우 드라이버는 정확한 행 수 또는 대략적인 행 수를 지원할 수 있지만 둘 다 지원할 수는 없습니다. 드라이버가 특정 커서 유형에 대해 정확한 행 과 근사 행 수를 지원하지 않는 경우 SQL_DIAG_CURSOR_ROW_COUNT 필드에는 지금까지 가져온 행 수가 포함됩니다. 드라이버가 지원하는 내용에 관계없이 SQL_FETCH_LAST *작업을* 사용하여 **SQLFetchScroll는** SQL_DIAG_CURSOR_ROW_COUNT 필드에 정확한 행 수를 포함하게 됩니다.
