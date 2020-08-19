---
description: 책갈피 형식
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e85d50a5fe3c21707a78ac2572d8a96166745319
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476815"
---
# <a name="bookmark-types"></a>책갈피 형식
ODBC 3.x의 모든 책갈피는 가변 길이 책갈피 *입니다.* 이렇게 하면 테이블에 연결 된 기본 키 또는 고유 인덱스를 책갈피로 사용할 수 있습니다. 또한 ODBC 2.x에서 사용 된 것 처럼 책갈피는 32 비트 값일 수 *있습니다.* 커서와 함께 책갈피를 사용 하도록 지정 하기 *위해 ODBC 2.x* 응용 프로그램은 SQL_ATTR_USE_BOOKMARK statement 특성을 SQL_UB_VARIABLE 설정 합니다. 가변 길이 책갈피가 자동으로 사용 됩니다.  
  
 응용 프로그램은 SQL_DESC_OCTET_LENGTH로 설정 된 *FieldIdentifier* 인수를 사용 하 여 **sqlcolattribute** 를 호출 하 여 책갈피의 길이를 가져올 수 있습니다. 가변 길이 책갈피는 long 값일 수 있으므로 응용 프로그램은 행 집합의 여러 행에 책갈피를 사용 하는 경우를 제외 하 고는 열 0에 바인딩하지 않아야 합니다.  
  
 고정 길이 책갈피는 이전 버전과의 호환성을 위해서만 지원 됩니다. Odbc 2.x 드라이버를 사용 하 여 작업 하 *는 odbc* *2.X 응용 프로그램이* **SQLSetStmtOption** 를 호출 하 여 SQL_USE_BOOKMARKS를 SQL_UB_ON로 설정 하면 드라이버 관리자에서 SQL_UB_VARIABLE에 매핑됩니다. 32 비트만 채워지는 경우에도 가변 길이 책갈피가 사용 됩니다. 드라이버가 고정 길이 책갈피를 지 원하는 경우 가변 길이 책갈피를 지원 합니다. Odbc 2.x 드라이버를 사용 하 여 작업 하 *는 odbc* *2.X 응용 프로그램이* **SQLSetStmtAttr** 를 호출 하 여 SQL_ATTR_USE_BOOKMARKS를 SQL_UB_VARIABLE로 설정 하면 드라이버 관리자에서 SQL_UB_ON으로 매핑되고 32 비트 고정 길이 책갈피가 사용 됩니다. 그런 다음 SQL_ATTR_FETCH_BOOKMARK_PTR statement 특성은 32 비트 책갈피를 가리켜야 합니다. 기본 키가 책갈피로 사용 되는 경우와 같이 사용 되는 책갈피가 32 비트 보다 길면 커서는 실제 값을 32 비트 값으로 매핑해야 합니다. 예를 들어 해시 테이블을 빌드할 수 있습니다. Odbc 2.x *드라이버를* 사용 하 여 작업 하는 odbc *2.x 응용 프로그램이* 책갈피를 바인딩하는 경우 버퍼 길이는 4 여야 합니다.
