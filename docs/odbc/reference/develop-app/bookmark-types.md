---
title: 책갈피 유형 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26d0297cd9dc57e9f30945a9248b235ae469da3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306334"
---
# <a name="bookmark-types"></a>책갈피 형식
ODBC *3.x의* 모든 책갈피는 가변 길이 책갈피입니다. 이렇게 하면 테이블과 연결된 기본 키 또는 고유 인덱스를 책갈피로 사용할 수 있습니다. 책갈피는 ODBC *2.x에서*사용된 것처럼 32비트 값일 수도 있습니다. 책갈피를 커서와 함께 사용하도록 지정하기 위해 ODBC *3.x* 응용 프로그램은 SQL_ATTR_USE_BOOKMARK 문 특성을 SQL_UB_VARIABLE 설정합니다. 가변 길이 책갈피가 자동으로 사용됩니다.  
  
 응용 프로그램은 책갈피의 길이를 얻기 위해 SQL_DESC_OCTET_LENGTH 설정된 *FieldIdentifier* 인수를 사용하여 **SQLColAttribute를** 호출할 수 있습니다. 가변 길이의 책갈피는 긴 값일 수 있으므로 행 집합의 많은 행에 대해 책갈피를 사용하지 않는 한 응용 프로그램은 열 0에 바인딩되지 않아야 합니다.  
  
 고정 길이 책갈피는 이전 버전과의 호환성에 대해서만 지원됩니다. ODBC *3.x* 드라이버로 작업하는 ODBC *2.x* 응용 프로그램이 **SQLSetStmtOption을** 호출하여 SQL_USE_BOOKMARKS SQL_UB_ON 설정하면 드라이버 관리자에서 SQL_UB_VARIABLE 매핑됩니다. 32비트만 채워져 있더라도 가변 길이의 책갈피를 사용합니다. 드라이버가 고정 길이 책갈피를 지원하는 경우 가변 길이 책갈피를 지원합니다. ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램이 **SQLSetStmtAttr을** 호출하여 SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE 설정하는 경우 드라이버 관리자에서 SQL_UB_ON 매핑되고 32비트 고정 길이 책갈피를 사용합니다. 그런 다음 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성은 32비트 책갈피를 가리킨다. 사용된 책갈피가 기본 키를 책갈피로 사용하는 경우와 같이 32비트보다 긴 경우 커서는 실제 값을 32비트 값에 매핑해야 합니다. 예를 들어 해시 테이블을 작성할 수 있습니다. ODBC *2.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램이 책갈피를 바인딩하는 경우 버퍼 길이는 4여야 합니다.
