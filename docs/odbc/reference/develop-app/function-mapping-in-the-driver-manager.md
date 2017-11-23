---
title: "드라이버 관리자는 매핑 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 63c908b668e4cecd93cc9930f638ccde9173b563
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="function-mapping-in-the-driver-manager"></a>함수 매핑 드라이버 관리자에서
드라이버 관리자는 문자열 인수를 사용 하는 함수에 대 한 두 진입점을 지원 합니다. 데코 레이트 되지 않은 함수 (**SQLDriverConnect**)은 ANSI 형식 함수입니다. 유니코드 형식으로 데코레이팅되 어는 *W* (**: SQLDriverConnectW**.)  
  
 ODBC 헤더 파일에서는로 데코 레이트 된 함수는 *A,* (**: SQLDriverConnectA**) 혼합된 ANSI/유니코드 응용 프로그램의 편의 위해 합니다. 에 대 한 호출에서 **A** 함수는 데코 레이트 되지 않은 진입점을 실제로 호출 (**SQLDriverConnect**.)  
  
 _UNICODE를 사용 하 여 응용 프로그램은 컴파일한 **#define**, ODBC 헤더 파일에는 데코 레이트 되지 않은 함수 호출 매핑됩니다 (**SQLDriverConnect**)을 유니코드 버전 (**: SQLDriverConnectW** .)  
  
 드라이버 관리자 경우 유니코드 드라이버는 드라이버 인식 **SQLConnectW** 드라이버에서 지원 됩니다.  
  
 드라이버 유니코드 드라이버, 드라이버 관리자에 게 함수 호출 다음과 같습니다.  
  
-   드라이버에 문자열 인수 또는 매개 변수 없이 함수를 통해 직접 전달합니다.  
  
-   유니코드 함수에 전달 (으로 *W* 접미사) 통해 직접 드라이버에 있습니다.  
  
-   ANSI 함수 변환 (으로 *A* 접미사) 유니코드 함수에 (으로 *W* 접미사) 문자열 인수를 유니코드로 변환 하 여 문자 및 유니코드 함수 드라이버에 전달 합니다.  
  
 드라이버 ANSI 드라이버, 드라이버 관리자에 게 함수 호출 다음과 같습니다.  
  
-   드라이버를 통해 직접를 매개 변수 또는 문자열 인수 없이 함수를 전달합니다.  
  
-   유니코드 함수 변환 (으로 *W* 접미사) ansi 함수 호출 하 고 드라이버에 전달 합니다.  
  
-   드라이버는 ANSI 함수 직접 전달합니다.  
  
 드라이버 관리자는 유니코드를 지원 내부적으로 합니다. 결과적으로 최적의 성능을 얻을 유니코드 드라이버를 사용 하는 유니코드 응용 프로그램에서 드라이버 관리자는 단순히 유니코드 함수를 통해 드라이버에 전달 하기 때문입니다. ANSI 응용 프로그램은 ANSI 드라이버를 사용할 때 드라이버 관리자에서에서 변환 해야 문자열 ANSI 유니코드와 같은 일부 함수를 처리할 때 **SQLDriverConnect**합니다. 함수를 처리 한 후 드라이버 관리자는 다음 변환 해야 유니코드 문자열 다시 ANSI로 함수를 ANSI 드라이버에 보내기 전에 합니다.  
  
 응용 프로그램은 수정 하거나 드라이버 SQL_NEED_DATA 또는 SQL_STILL_EXECUTING을 반환 하는 경우의 바인딩된 매개 변수 버퍼에 읽을 수입니다. 드라이버 관리자 드라이버가 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO 또는 sql_error가 반환 될 때까지 ANSI에 바인딩된 버퍼를 유지 합니다. 다중 스레드 응용 프로그램에 다른 스레드가에 SQL 문을 실행 하는 모든 바인딩된 매개 변수 값에 액세스 해야 합니다. 드라이버 관리자는 데이터에서 유니코드 "위치"에서 ANSI로 변환한 드라이버에서 SQL 문을 처리 하는 동안 다른 스레드가 이러한 버퍼에 ANSI 데이터를 볼 수 있습니다. 유니코드 데이터는 ANSI 드라이버를 바인딩하는 응용 프로그램은 동일한 주소를 두 개의 다른 열을 바인딩해야 합니다.
