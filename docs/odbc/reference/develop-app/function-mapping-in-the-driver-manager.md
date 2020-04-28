---
title: 드라이버 관리자의 함수 매핑 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305584"
---
# <a name="function-mapping-in-the-driver-manager"></a>드라이버 관리자의 함수 매핑
드라이버 관리자는 문자열 인수를 사용 하는 함수에 대 한 두 가지 진입점을 지원 합니다. 데코레이팅되지 않은 함수 (**SQLDriverConnect**)는 함수의 ANSI 형식입니다. 유니코드 형식은 *W* (**: sqldriverconnectw**)로 데코 레이트 됩니다.  
  
 ODBC 헤더 파일은 혼합 ANSI/유니코드 응용 프로그램의 편의를 위해 *A,* (**: sqldriverconnecta**)로 데코레이팅된 함수도 지원 합니다. **함수에 대 한 호출은** 실제로 데코레이팅되지 않은 진입점 (**SQLDriverConnect**)을 호출 합니다.  
  
 응용 프로그램이 _UNICODE **#define**를 사용 하 여 컴파일되면 ODBC 헤더 파일은 데코레이팅되지 않은 함수 호출 (**SQLDriverConnect**)을 유니코드 버전 (**: sqldriverconnectw**)에 매핑합니다.  
  
 드라이버 관리자는 드라이버에서 **Sqlconnectw** 를 지 원하는 경우 드라이버를 유니코드 드라이버로 인식 합니다.  
  
 드라이버가 유니코드 드라이버 이면 드라이버 관리자는 다음과 같이 함수 호출을 수행 합니다.  
  
-   문자열 인수 또는 매개 변수가 없는 함수를 드라이버에 직접 전달 합니다.  
  
-   *접두사를 사용 하 여 유니코드* 함수를 드라이버에 직접 전달 합니다.  
  
-   문자열 인수를 유니코드 문자로 변환 하 고 유니코드 함수를 드라이버에 전달 하 여 ANSI 함수 *(접미사 포함* )를 유니코드 함수 ( *W* 접미사 포함)로 변환 합니다.  
  
 드라이버가 ANSI 드라이버 이면 드라이버 관리자는 다음과 같이 함수 호출을 수행 합니다.  
  
-   문자열 인수 또는 매개 변수 없이 함수를 드라이버에 직접 전달 합니다.  
  
-   유니코드 함수 ( *W* 접미사 포함)를 ANSI 함수 호출로 변환 하 여 드라이버에 전달 합니다.  
  
-   ANSI 함수를 드라이버에 직접 전달 합니다.  
  
 드라이버 관리자는 내부적으로 유니코드를 사용할 수 있습니다. 따라서 드라이버 관리자가 유니코드 함수를 드라이버에 전달 하기 때문에 유니코드 드라이버를 사용 하는 유니코드 응용 프로그램에서 최적의 성능을 얻을 수 있습니다. Ansi 응용 프로그램에서 ANSI 드라이버를 사용 하는 경우 **SQLDriverConnect**와 같은 일부 함수를 처리할 때 드라이버 관리자가 Ansi에서 유니코드로 변환 해야 합니다. 함수를 처리 한 후 드라이버 관리자는 ANSI 드라이버로 함수를 전송 하기 전에 유니코드 문자열을 다시 ANSI로 변환 해야 합니다.  
  
 드라이버가 SQL_STILL_EXECUTING 또는 SQL_NEED_DATA를 반환할 때 응용 프로그램에서 바인딩된 매개 변수 버퍼를 수정 하거나 읽지 않아야 합니다. 드라이버 관리자는 드라이버가 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR를 반환할 때까지 ANSI에 바인딩된 버퍼를 유지 합니다. 다중 스레드 응용 프로그램은 다른 스레드에서 SQL 문을 실행 하는 바인딩된 매개 변수 값에 대 한 액세스 권한을 얻을 수 없습니다. 드라이버 관리자는 데이터를 유니코드에서 ANSI "내부"로 변환 하 고, 다른 스레드는 드라이버에서 여전히 SQL 문을 처리 하는 동안 이러한 버퍼의 ANSI 데이터를 볼 수 있습니다. 유니코드 데이터를 ANSI 드라이버에 바인딩하는 응용 프로그램은 두 개의 서로 다른 열을 동일한 주소에 바인딩하지 않아야 합니다.
