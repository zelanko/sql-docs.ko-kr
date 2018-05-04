---
title: 유니코드 데이터 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7871576f95ebb49708036d531c4f2d8eebbac863
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="unicode-data"></a>유니코드 데이터
SQL 유니코드 데이터 형식은 고유 하 게 하는 DBMS에서 유니코드로에 있는 데이터를 설명 하기 위해 제공 됩니다. C 유니코드 데이터 형식은 응용 프로그램 데이터를 유니코드 버퍼에 바인딩할 수 있도록 제공 됩니다. 드라이버 관리자 유니코드 C 형식 있도록 (SQL_C_WCHAR)에서 데이터를 변환할 수는 ANSI 드라이버로 함수입니다.  
  
 ODBC 3.0 또는 2입니다. *x* 응용 프로그램은 항상 ANSI 데이터 형식에 바인딩합니다. 최적의 성능을 얻으려면 이러한 ODBC 3.5 (또는 이상) 응용 프로그램 SQL 열 형식은 ansi SQL 열 형식은 유니코드 이면 유니코드 C 데이터 형식에 바인딩해야 하는 경우 ANSI C 데이터 형식에 바인딩해야 합니다.  
  
 SQL 유니코드 형식 표시기 SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR 됩니다. SQL_WCHAR 데이터 SQL_WVARCHAR에 선언 된 최대 가변 길이 있고 SQL_WLONGVARCHAR 데이터 원본에 의존 하는 최대 가변 길이 동안 고정된 문자열 길이 있습니다.  
  
 C 유니코드 유형 표시기가 SQL_C_WCHAR 합니다. 각 SQL 유니코드 형식 표시기에 대 한 기본값입니다. 모든 SQL 유형이 SQL_C_WCHAR로 변환할 수 SQL_C_WCHAR 모든 SQL 형식에 변환 될 수 있습니다. 응용 프로그램 세 가지 방법 중 하나로 데이터를 검색할 수 있습니다.  
  
-   SQL_C_CHAR로 데이터를 검색 합니다.  
  
-   SQL_C_WCHAR로 데이터를 검색 합니다.  
  
-   SQL_C_TCHAR로 데이터를 선언 합니다. 응용 프로그램이 유니코드 응용 프로그램으로 컴파일된 또는 ANSI 응용 프로그램으로 컴파일할 경우 SQL_C_CHAR를 삽입 하는 경우 SQL_C_WCHAR를 삽입 하는 매크로입니다.  
  
 SQL_C_TCHAR 함수에서 다음과 같이 선언 됩니다.  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 응용 프로그램이 유니코드 응용 프로그램으로 컴파일될 때는 *ValueType* 인수 SQL_C_TCHAR에서 SQL_C_WCHAR로 변경 합니다. ANSI 응용 프로그램으로 응용 프로그램을 컴파일할 때는 *ValueType* 인수 SQL_C_CHAR 변경 합니다.  
  
 유니코드 드라이버 ANSI 데이터 형식에 SQL_CHAR 에서도 지원 해야 합니다. 유니코드 드라이버로 작업 하는 응용 프로그램 SQL_CHAR를 바인딩할 경우 드라이버 관리자 SQL_CHAR 데이터 SQL_WCHAR에에 매핑되지 않습니다. 유니코드 드라이버 SQL_CHAR 데이터 동의 해야 합니다.  
  
 드라이버 관리자는 유니코드로 드라이버 및 DSN 이름을 저장 하 고 필요에 따라 ANSI로 매핑합니다. 변환 될 수 없는 문자는 기본 문자 sup으로 표현 됩니다 (컴퓨터의 네이티브 코드 페이지 하지 않은 코드 페이지 드라이버 및 DSN 이름에 사용 되는 경우 발생할 수 있습니다) 처럼를 ANSI 문자로 유니코드 문자를 매핑할 수 없으면, 시스템에서 plied 합니다.
