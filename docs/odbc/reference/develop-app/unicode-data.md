---
title: 유니코드 데이터 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74de6c44aaf109a434f0cf76c6902abfba92efe1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305767"
---
# <a name="unicode-data"></a>유니코드 데이터
SQL 유니코드 데이터 형식은 유니코드에서 DBMS에 있는 데이터를 설명 하기 위해 제공 됩니다. C 유니코드 데이터 형식은 유니코드 버퍼에 데이터 바인딩 응용 프로그램을 허용 하도록 제공 됩니다. 드라이버 관리자 (SQL_C_WCHAR) 있도록 유니코드 C 형식에서 데이터를 변환할 수는 ANSI 드라이버를 사용 하 여 함수입니다.  
  
 ODBC 3.0 또는 2입니다. *x* 응용 프로그램에 항상 ANSI 데이터 형식에 바인딩됩니다. 최적의 성능을 얻으려면 이러한 ODBC 3.5 (또는 이상) 응용 프로그램 SQL 열 형식이 ansi SQL 열 형식은 유니코드 경우 유니코드 C 데이터 형식에 바인딩해야 하는 경우 ANSI C 데이터 형식에 바인딩해야 합니다.  
  
 SQL Unicode 형식 표시기 SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR 됩니다. SQL_WCHAR 데이터 길이가 고정된 문자열, SQL_WVARCHAR 선언 된 최대 변수 길이가 고 SQL_WLONGVARCHAR 데이터 원본에 따라 달라 지는 최대 가변 길이입니다.  
  
 C 유니코드 유형 표시기가 SQL_C_WCHAR 합니다. 이것은 각 SQL Unicode 형식 표시기에 대 한 기본값입니다. SQL_C_WCHAR로 변환할 수는 SQL 유형의 모든 SQL_C_WCHAR SQL 형식의 모든 변환 될 수 있습니다. 응용 프로그램에는 세 가지 방법 중 하나에서 데이터가 검색할 수 있습니다.  
  
-   SQL_C_CHAR로 데이터를 검색 합니다.  
  
-   SQL_C_WCHAR로 데이터를 검색 합니다.  
  
-   SQL_C_TCHAR로 데이터를 선언 합니다. 이 응용 프로그램은 유니코드 응용 프로그램으로 컴파일되거나 ANSI 응용 프로그램으로 컴파일된 경우 SQL_C_CHAR 삽입 SQL_C_WCHAR 삽입 하는 매크로입니다.  
  
 SQL_C_TCHAR 함수에서 다음과 같이 선언 됩니다.  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 유니코드 응용 프로그램의 경우 응용 프로그램 컴파일시 합니다 *ValueType* 인수 SQL_C_TCHAR에서 SQL_C_WCHAR로 변경 됩니다. ANSI 응용 프로그램으로 응용 프로그램 컴파일시 합니다 *ValueType* 인수 SQL_C_CHAR로 변경 됩니다.  
  
 유니코드 드라이버 SQL_CHAR를 포함 하 여 ANSI 데이터 형식 지원 해야 합니다. 유니코드 드라이버에서 작동 하는 응용 프로그램 SQL_CHAR를 바인딩할 경우 드라이버 관리자 SQL_CHAR 데이터 SQL_WCHAR에에 매핑되지 않습니다. 유니코드 드라이버 SQL_CHAR 데이터 동의 해야 합니다.  
  
 드라이버 관리자는 유니코드로 드라이버 이름과 DSN 저장 하 고 필요에 따라 ANSI로 매핑합니다. 기본 문자 sup 나타내는 변환할 수 없는 문자를 유니코드 문자를 ANSI 문자로 (드라이버 및 DSN 이름 문자는 컴퓨터의 기본 코드 페이지를 하지 않은 코드 페이지를 사용 하는 경우 발생할 수 있습니다)으로 매핑할 수 없습니다, 하는 경우 시스템에서 plied 합니다.
