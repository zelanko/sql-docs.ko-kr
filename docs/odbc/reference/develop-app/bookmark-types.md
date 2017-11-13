---
title: "형식에 책갈피 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a4ab42d7a8b18ebb2b37c871f46981c69c84b908
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="bookmark-types"></a>책갈피 형식
ODBC 3에서 모든 책갈피*.x* 가변 길이 책갈피가 합니다. 이렇게 하면 기본 키 또는 책갈피도 사용할 테이블에 연결 된 고유 인덱스가 있습니다. 책갈피 수도 있습니다는 32 비트 값 ODBC 2에 사용 되었습니다. *x*합니다. 커서를 ODBC 3 책갈피 사용 되도록 지정 하려면*.x* 응용 프로그램 SQL_UB_VARIABLE를 SQL_ATTR_USE_BOOKMARK 문 특성을 설정 합니다. 가변 길이 책갈피 자동으로 사용 됩니다.  
  
 응용 프로그램에서 호출할 수 **SQLColAttribute** 와 *FieldIdentifier* 인수는 책갈피의 길이를 가져오려면 SQL_DESC_OCTET_LENGTH로 설정 합니다. 가변 길이 책갈피는 long 값 일 수 있으므로 응용 프로그램 해야에 바인딩할 열 0 않으면 여러 행 집합의 행에 대 한 책갈피를 사용 합니다.  
  
 고정 길이의 책갈피는 이전 버전과 호환성을 위해서만 지원 됩니다. 경우에는 ODBC 2입니다. *x* ODBC 3을 사용 하는 응용 프로그램*.x* 드라이버 호출 **SQLSetStmtOption** 드라이버 관리자 SQL_UB_VARIABLE 매핑 SQL_USE_BOOKMARKS SQL_UB_ON을 설정 하려면 . 가변 길이 책갈피의 32 비트만 채워지는 경우에 사용 됩니다. 드라이버 고정 길이의 책갈피를 지 원하는 경우에 가변 길이 책갈피를 지원 합니다. ODBC 3 경우*.x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 호출 **SQLSetStmtAttr** SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE을 설정 하려면 드라이버 관리자 SQL_UB_ON 매핑 및 32 비트 고정 길이의 책갈피를 사용 합니다. SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성을 32 비트 책갈피로 다음 가리켜야 합니다. 사용 되는 책갈피는 책갈피로, 기본 키를 사용할 때와 같은 32 비트 보다 긴 경우 커서에 32 비트 값에 실제 값이 매핑해야 합니다. 예를 들어, 그 중 해시 테이블을 작성할 수 것입니다. ODBC 3 때*.x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 바인딩합니다 책갈피, 버퍼 길이 4 이어야 합니다.

