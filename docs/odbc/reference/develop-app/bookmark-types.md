---
title: 책갈피 유형 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9aca006623d9ddb8292147d8a28c93f912fd25d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794016"
---
# <a name="bookmark-types"></a>책갈피 형식
ODBC에서 모든 책갈피 *3.x* 가변 길이 책갈피 됩니다. 이 기본 키 또는 책갈피로 사용할 테이블과 연결 된 고유 인덱스를 허용 합니다. 책갈피 수도 있습니다는 32 비트 값 ODBC에서 사용 된 *2.x*합니다. 책갈피는 ODBC 커서에 사용 됨을 지정 하려면 *3.x* SQL_UB_VARIABLE를 SQL_ATTR_USE_BOOKMARK 문 특성을 설정 하는 응용 프로그램입니다. 가변 길이 책갈피 자동으로 사용 됩니다.  
  
 응용 프로그램에서 호출할 수 있습니다 **SQLColAttribute** 사용 하 여 합니다 *FieldIdentifier* 인수는 책갈피의 길이 가져오려면 SQL_DESC_OCTET_LENGTH로 설정 합니다. 가변 길이 책갈피는 long 값을 일 수 있으므로 여러 행 집합의 행에 대 한 책갈피를 사용 하지 않는 한 응용 프로그램 해야 하지 0 열에 바인딩됩니다.  
  
 고정 길이 책갈피는 이전 버전과 호환성을 위해서만 지원 됩니다. 경우 ODBC *2.x* ODBC를 사용 하는 응용 프로그램 *3.x* 드라이버 호출 **SQLSetStmtOption** SQL_USE_BOOKMARKS SQL_UB_ON을 설정 하려면 SQL_에 드라이버 관리자의 매핑 UB_VARIABLE 합니다. 가변 길이 책갈피의 32 비트에 불과하지만 채워지는 경우에 사용 됩니다. 드라이버를 고정 길이 책갈피를 지 원하는 경우에 가변 길이 책갈피를 지원 합니다. 경우 ODBC *3.x* ODBC를 사용 하는 응용 프로그램 *2.x* 드라이버 호출 **SQLSetStmtAttr** SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS로 매핑되는 드라이버 관리자 SQL_UB_ON 및 32 비트 고정 길이 책갈피에 사용 됩니다. 다음은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성은 32 비트 책갈피 가리켜야 합니다. 사용 되는 책갈피는 책갈피와 기본 키가 사용 하는 경우 같은 32 비트 보다 긴 경우 커서 32 비트 값을 실제 값을 매핑해야 합니다. 예를 들어,의 해시 테이블을 작성할 수, 해당. 때 ODBC *3.x* ODBC를 사용 하는 응용 프로그램 *2.x* 드라이버 바인딩합니다 책갈피, 버퍼 길이 4 여야 합니다.
