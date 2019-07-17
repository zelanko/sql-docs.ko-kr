---
title: 드라이버 관리자의 매핑 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2bfa535d4175c109e96098dd1e40e93be9521de2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069696"
---
# <a name="function-mapping-in-the-driver-manager"></a>드라이버 관리자의 함수 매핑
드라이버 관리자는 문자열 인수를 사용 하는 함수에 대 한 두 진입점을 지원 합니다. 데코 레이트 되지 않은 함수 (**SQLDriverConnect**) 함수의 ANSI 형식입니다. 유니코드 형식으로 데코 레이트 된를 *W* ( **: SQLDriverConnectW**.)  
  
 ODBC 헤더 파일에는 또한 데코 레이트 하는 함수 지원를 *A* ( **: SQLDriverConnectA**) 혼합 된 ANSI/유니코드 응용 프로그램의 편의 위해. 호출을 **A** 함수는 데코 레이트 되지 않은 진입점에 대 한 호출은 실제로 (**SQLDriverConnect**.)  
  
 응용 프로그램은 _UNICODE를 사용 하 여 컴파일된 경우 **#define**, ODBC 헤더 파일을 데코 레이트 되지 않은 함수 호출을 매핑하는 (**SQLDriverConnect**)를 유니코드 버전 ( **: SQLDriverConnectW** .)  
  
 드라이버 관리자 경우 유니코드 드라이버를 드라이버 인식 **SQLConnectW** 드라이버에서 지원 됩니다.  
  
 드라이버는 유니코드 드라이버를 드라이버 관리자 함수 호출을 다음과 같이 하면:  
  
-   드라이버에 문자열 인수 또는 매개 변수 없이 함수를 통해 직접 전달합니다.  
  
-   유니코드 함수에 전달 (사용 하 여 합니다 *W* 접미사) 통해 직접 드라이버입니다.  
  
-   ANSI 함수 변환 (사용 하 여는 *는* 접미사) 유니코드 함수 (사용 하 여는 *W* 접미사) 문자열 인수를 유니코드로 변환 하 여 문자 및 유니코드 함수 드라이버를 전달 합니다.  
  
 드라이버는 ANSI 드라이버를 드라이버 관리자 함수 호출을 다음과 같이 하면:  
  
-   드라이버를 통해 직접를 매개 변수 또는 문자열 인수 없이 함수를 전달합니다.  
  
-   유니코드 함수 변환 (사용 하 여 합니다 *W* 접미사) ansi 함수 호출 및 드라이버에 전달 합니다.  
  
-   드라이버는 ANSI 함수 직접 전달합니다.  
  
 드라이버 관리자는 유니코드 지원 내부적으로 합니다. 결과적으로 드라이버 관리자 드라이버를 통해 유니코드 함수는 단순히 전달 하므로 유니코드 드라이버를 사용 하는 유니코드 응용 프로그램에서 최적의 성능은 가져옵니다. ANSI 응용 프로그램에는 ANSI 드라이버에서 작업할 때 드라이버 관리자에서에서 변환 해야 문자열 ANSI 유니코드와 같은 일부 함수를 처리 하는 동안 **SQLDriverConnect**합니다. 함수를 처리 한 후 드라이버 관리자 해야 다음 유니코드 문자열 다시 ANSI로 변환 ANSI 드라이버에 함수를 보내기 전에 합니다.  
  
 응용 프로그램을 수정 하거나 드라이버 SQL_NEED_DATA 또는 SQL_STILL_EXECUTING을 반환 하는 경우 해당 바인딩된 매개 변수 버퍼를 읽기 하지 해야 합니다. 드라이버 관리자는 드라이버는 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO 또는 sql_error가 반환 될 때까지 ANSI로 바인딩된 버퍼를 유지 합니다. 다중 스레드 응용 프로그램을에 다른 스레드가에서 SQL 문을 실행 되는 모든 바인딩된 매개 변수 값에 액세스 해야 합니다. 드라이버 관리자는 유니코드에서 "위치"에서 ANSI로 데이터를 변환 하 고 드라이버 SQL 문을 계속 처리 하는 동안 다른 스레드가 이러한 버퍼에 ANSI 데이터를 표시 될 수 키를 누릅니다. 유니코드 데이터는 ANSI driver를 바인딩하는 응용 프로그램 같은 주소로 두 개의 다른 열을 바인딩해야 합니다.
