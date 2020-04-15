---
title: 드라이버 관리자의 함수 매핑 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db8e525bb7e8f3e167deb8061a4dd5b75073933c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305584"
---
# <a name="function-mapping-in-the-driver-manager"></a>드라이버 관리자의 함수 매핑
드라이버 관리자는 문자열 인수를 취하는 함수에 대해 두 가지 진입점을 지원합니다. 데코레이팅되지 않은**함수(SQLDriverConnect)는**함수의 ANSI 형식입니다. 유니코드 양식은**W(SQLDriverConnectW)로**장식되어 있습니다. *W*  
  
 ODBC 헤더 파일은 혼합 ANSI/유니코드 응용 프로그램의 편의를 위해**A(SQLDriverConnectA)로**장식된 기능도 지원합니다. *A,* **A** 함수에 대한 호출은 실제로 장식되지 않은 진입점(SQLDriverConnect.) 호출입니다.**SQLDriverConnect**  
  
 응용 프로그램이 **#define**_UNICODE 컴파일되는 경우 ODBC 헤더 파일은 장식되지 않은 함수**호출(SQLDriverConnect)을**유니코드**버전(SQLDriverConnectW)에**매핑합니다.  
  
 드라이버 관리자는 **SQLConnectW가** 드라이버에서 지원되는 경우 드라이버를 유니코드 드라이버로 인식합니다.  
  
 드라이버가 유니코드 드라이버인 경우 드라이버 관리자는 다음과 같이 함수 호출을 수행합니다.  
  
-   문자열 인수 또는 매개 변수없이 함수를 드라이버에 직접 전달합니다.  
  
-   *유니코드 함수(W* 접미사 사용)를 드라이버에 직접 전달합니다.  
  
-   문자열 인수를 유니코드 문자로 변환하여 ANSI *함수(A* 접미사 사용)를 유니코드 *함수(W* 접미사 사용)로 변환하고 유니코드 함수를 드라이버에 전달합니다.  
  
 드라이버가 ANSI 드라이버인 경우 드라이버 관리자는 다음과 같이 함수 호출을 수행합니다.  
  
-   문자열 인수 나 매개 변수없이 함수를 드라이버로 직접 전달합니다.  
  
-   유니코드 *함수(W* 접미사 사용)를 ANSI 함수 호출로 변환하고 드라이버에 전달합니다.  
  
-   ANSI 함수를 드라이버에 직접 전달합니다.  
  
 드라이버 관리자는 내부적으로 유니코드로 활성화되어 있습니다. 따라서 드라이버 관리자는 유니코드 함수를 드라이버로 전달하기 때문에 유니코드 드라이버로 작업하는 유니코드 응용 프로그램에서 최적의 성능을 얻을 수 있습니다. ANSI 응용 프로그램이 ANSI 드라이버로 작업하는 경우 드라이버 관리자는 **SQLDriverConnect**와 같은 일부 기능을 처리할 때 ANSI에서 유니코드로 문자열을 변환해야 합니다. 함수를 처리한 후 드라이버 관리자는 ANSI 드라이버로 함수를 보내기 전에 유니코드 문자열을 ANSI로 다시 변환해야 합니다.  
  
 응용 프로그램은 드라이버가 SQL_STILL_EXECUTING 반환하거나 SQL_NEED_DATA 때 바인딩된 매개 변수 버퍼를 수정하거나 읽지 않아야 합니다. 드라이버 관리자는 드라이버가 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR 반환할 때까지 ANSI에 바인딩된 버퍼를 남깁니다. 다중 스레드 응용 프로그램은 다른 스레드가 SQL 문을 실행하는 바인딩된 매개 변수 값에 액세스해서는 안 됩니다. 드라이버 관리자는 유니코드의 데이터를 ANSI로 "제자리에" 변환하고 다른 스레드는 드라이버가 SQL 문을 처리하는 동안 이러한 버퍼에 ANSI 데이터를 볼 수 있습니다. 유니코드 데이터를 ANSI 드라이버에 바인딩하는 응용 프로그램은 두 개의 서로 다른 열을 동일한 주소에 바인딩할 수 없습니다.
