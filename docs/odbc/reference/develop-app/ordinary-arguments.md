---
title: "일반 인수 | Microsoft Docs"
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
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9aaaa374817d84eaa01dc96fa3783623e7b4b905
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="ordinary-arguments"></a>일반 인수
카탈로그 함수 문자열 인수는 일반 인수를 리터럴 문자열로 처리 됩니다. 검색 패턴은 문자열도 아니고 값 목록이 일반 인수를 허용합니다. 일반 인수는 대/소문자는 중요, 및 문자열에 인용 문자는 문자 그대로 해석 됩니다. 이 인수 SQL_ATTR_METADATA_ID 문 특성은 SQL_FALSE;로 설정 하는 경우 일반 인수도 간주 됩니다. 로 간주 됩니다 식별자 인수 대신이 특성은 SQL_TRUE로 설정 하는 경우.  
  
 Null 포인터는 일반 인수를 설정 하 고 인수는 필수 인수를 함수 반환 SQL_ERROR 및 SQLSTATE HY009 (null 포인터를 잘못 사용). Null 포인터는 일반 인수를 설정 하는 경우 인수가 필수 인수는 인수 동작은 드라이버에 따라 다릅니다. 필수 인수는 다음과 같습니다.  
  
|함수|필수 인수|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*테이블 이름*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*테이블 이름*|  
|**SQLSpecialColumns**|*테이블 이름*|  
|**SQLStatistics**|*테이블 이름*|
