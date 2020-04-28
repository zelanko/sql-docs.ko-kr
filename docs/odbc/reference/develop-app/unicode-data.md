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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73ea9035b05f04fec1527ca2aa98531a807db8cf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307400"
---
# <a name="unicode-data"></a>유니코드 데이터
SQL 유니코드 데이터 형식은 기본적으로 DBMS에 있는 유니코드로 된 데이터를 설명 하기 위해 제공 됩니다. 응용 프로그램이 유니코드 버퍼에 데이터를 바인딩할 수 있도록 하는 C 유니코드 데이터 형식이 제공 됩니다. 드라이버 관리자는 ANSI 드라이버를 사용할 수 있도록 유니코드 C 형식 (SQL_C_WCHAR)에서 데이터를 변환할 수 있습니다.  
  
 ODBC 3.0 또는 2. *x* 응용 프로그램은 항상 ANSI 데이터 형식에 바인딩됩니다. 최적의 성능을 위해서는 SQL 열 유형이 ANSI 인 경우 ODBC 3.5 이상 응용 프로그램을 ANSI 데이터 C 유형에 바인딩해야 하며, SQL 열 유형이 Unicode 인 경우에는 유니코드 C 데이터 형식에 바인딩해야 합니다.  
  
 SQL 유니코드 형식 표시기는 SQL_WCHAR, SQL_WVARCHAR 및 SQL_WLONGVARCHAR입니다. SQL_WCHAR 데이터의 문자열 길이는 고정 되어 있고 SQL_WVARCHAR는 가변 길이가 선언 된 최대값을 가진 가변 길이를 가지 며 SQL_WLONGVARCHAR에는 데이터 소스에 따라 달라 지는 최대의 가변 길이가 있습니다.  
  
 C 유니코드 형식 표시기가 SQL_C_WCHAR 됩니다. 이는 각각의 SQL 유니코드 형식 표시기에 대 한 기본값입니다. 모든 SQL 형식을 SQL_C_WCHAR 변환할 수 있으며 SQL_C_WCHAR 모든 SQL 형식으로 변환할 수 있습니다. 응용 프로그램은 다음 세 가지 방법 중 하나로 데이터를 검색할 수 있습니다.  
  
-   SQL_C_CHAR으로 데이터를 검색 합니다.  
  
-   SQL_C_WCHAR으로 데이터를 검색 합니다.  
  
-   데이터를 SQL_C_TCHAR으로 선언 합니다. 응용 프로그램을 유니코드 응용 프로그램으로 컴파일하거나 ANSI 응용 프로그램으로 컴파일된 경우 SQL_C_CHAR 삽입 하는 SQL_C_WCHAR 삽입 하는 매크로입니다.  
  
 SQL_C_TCHAR은 다음과 같이 함수에서 선언 됩니다.  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 응용 프로그램을 유니코드 응용 프로그램으로 컴파일하면 *ValueType* 인수가 SQL_C_TCHAR에서 SQL_C_WCHAR로 변경 됩니다. 응용 프로그램을 ANSI 응용 프로그램으로 컴파일하면 *ValueType* 인수가 SQL_C_CHAR로 변경 됩니다.  
  
 유니코드 드라이버는 SQL_CHAR을 포함 하 여 ANSI 데이터 형식을 계속 지원 해야 합니다. 유니코드 드라이버를 사용 하는 응용 프로그램이 SQL_CHAR에 바인딩되는 경우 드라이버 관리자는 SQL_CHAR 데이터를 SQL_WCHAR에 매핑하지 않습니다. 유니코드 드라이버는 SQL_CHAR 데이터를 수락 해야 합니다.  
  
 드라이버 관리자는 드라이버 및 DSN 이름을 유니코드로 저장 하 고 필요에 따라 ANSI에 매핑합니다. 유니코드 문자를 ANSI 문자에 매핑할 수 없는 경우 (컴퓨터의 네이티브 코드 페이지가 아닌 코드 페이지의 문자가 드라이버 및 DSN 이름에 사용 되는 경우에도 발생할 수 있음) 변환할 수 없는 문자는 시스템에서 제공 하는 기본 문자로 표시 됩니다.
