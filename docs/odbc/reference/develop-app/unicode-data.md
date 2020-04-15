---
title: 유니코드 데이터 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73ea9035b05f04fec1527ca2aa98531a807db8cf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307400"
---
# <a name="unicode-data"></a>유니코드 데이터
SQL 유니코드 데이터 형식은 기본적으로 DBMS에 유니코드에 있는 데이터를 설명하기 위해 제공됩니다. 응용 프로그램이 유니코드 버퍼에 데이터를 바인딩할 수 있도록 C 유니코드 데이터 형식이 제공됩니다. 드라이버 관리자는 유니코드 C 유형(SQL_C_WCHAR)의 데이터를 변환하여 ANSI 드라이버로 작동하도록 할 수 있습니다.  
  
 ODBC 3.0 또는 2. *x* 응용 프로그램은 항상 ANSI 데이터 형식에 바인딩됩니다. 최적의 성능을 위해 ODBC 3.5(또는 그 이상) 응용 프로그램은 SQL 열 형식이 ANSI인 경우 ANSI 데이터 C 형식에 바인딩해야 하며 SQL 열 형식이 유니코드인 경우 유니코드 C 데이터 형식에 바인딩해야 합니다.  
  
 SQL 유니코드 유형 표시기는 SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR. SQL_WCHAR 데이터는 고정 된 문자열 길이, SQL_WVARCHAR 선언 된 최대와 변수 길이 SQL_WLONGVARCHAR 데이터 원본에 따라 달라 집니다 최대변수 길이.  
  
 C 유니코드 유형 표시등이 SQL_C_WCHAR. 각 SQL 유니코드 유형 표시기의 기본값입니다. 모든 SQL 형식을 SQL_C_WCHAR 변환할 수 있으며 SQL_C_WCHAR 모든 SQL 유형으로 변환할 수 있습니다. 응용 프로그램은 다음 세 가지 방법 중 하나로 데이터를 검색할 수 있습니다.  
  
-   데이터를 SQL_C_CHAR 검색합니다.  
  
-   데이터를 SQL_C_WCHAR 검색합니다.  
  
-   데이터를 SQL_C_TCHAR 선언합니다. 응용 프로그램이 유니코드 응용 프로그램으로 컴파일되는 경우 SQL_C_WCHAR 삽입하거나 ANSI 응용 프로그램으로 컴파일되는 경우 SQL_C_CHAR 삽입하는 매크로입니다.  
  
 SQL_C_TCHAR 다음과 같이 함수에서 선언됩니다.  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 응용 프로그램이 유니코드 응용 프로그램으로 컴파일되면 *ValueType* 인수가 SQL_C_TCHAR SQL_C_WCHAR 변경됩니다. 응용 프로그램이 ANSI 응용 프로그램으로 컴파일되면 *ValueType* 인수가 SQL_C_CHAR 변경됩니다.  
  
 유니코드 드라이버는 SQL_CHAR 포함하여 ANSI 데이터 형식을 계속 지원해야 합니다. 유니코드 드라이버로 작업하는 응용 프로그램이 SQL_CHAR 바인딩하는 경우 드라이버 관리자는 SQL_WCHAR SQL_CHAR 데이터를 매핑하지 않습니다. 유니코드 드라이버는 SQL_CHAR 데이터를 수락해야 합니다.  
  
 드라이버 관리자는 드라이버와 DSN 이름을 유니코드에 저장하고 필요에 따라 ANSI에 매핑합니다. 유니코드 문자를 ANSI 문자에 매핑할 수 없는 경우(컴퓨터의 기본 코드 페이지가 아닌 코드 페이지의 문자가 드라이버 및 DSN 이름에 사용되는 경우 발생할 수 있음) 변환할 수 없는 문자는 시스템에서 제공하는 기본 문자로 표시됩니다.
