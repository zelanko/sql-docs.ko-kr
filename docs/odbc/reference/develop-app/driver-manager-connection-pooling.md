---
title: "드라이버 관리자 연결 풀링 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d2883c374768723eeff4100113873130eeea6da7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="driver-manager-connection-pooling"></a>드라이버 관리자 연결 풀링
연결 풀링은 사용할 때마다 다시 설정에 필요 하지 않은 연결 풀에서 연결을 사용 하도록 응용 프로그램입니다. 연결이 만들어지고 풀에 배치 된 후 응용 프로그램 전체 연결 프로세스를 수행 하지 않고 해당 연결 다시 사용할 수 있습니다.  
  
 풀링된 연결을 사용 하 여 응용 프로그램 연결 설정에 관련 된 오버 헤드를 줄일 수 때문에 성능이 크게 향상 될 수 있습니다. 이 네트워크를 통해 연결 하는 중간 계층 응용 프로그램 또는 반복적으로 연결 하 고 연결을 끊거나, 인터넷 응용 프로그램과 같은 응용 프로그램에 특히 중요 수 있습니다.  
  
 성능 향상 뿐만 아니라 연결 풀링 아키텍처에는 환경 및 해당 관련된 연결 단일 프로세스에서 여러 구성 요소에서 사용할 수 있습니다. 즉, 서로 인식 하지 않고 독립 실행형 구성 요소는 같은 프로세스에서 서로 상호 작용 수 있습니다. 여러 구성 요소는 연결 풀에서 연결을 반복적으로 사용할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 2를 표시 하는 ODBC 응용 프로그램에서 연결 풀링을 사용할 수 있습니다. *x* 동작을 응용 프로그램에서 호출할 수 만큼 *SQLSetEnvAttr*합니다. 응용 프로그램 데이터베이스 또는 데이터베이스를 변경 하는 등의 컨텍스트를 변경 하는 SQL 문을 실행 해서는 안 연결 풀링을 사용 하는 경우는 \< *데이터베이스**이름*> 역할 데이터 원본에 의해 사용 되는 카탈로그를 변경 합니다.  
  
 ODBC 드라이버는 완벽 하 게 스레드로부터 안전 해야 하 고 연결에는 연결 풀링을 지원 하도록 스레드 선호도 없어야 합니다. 즉, 드라이버는 언제 든 지 모든 스레드에서 호출을 처리할 수와 한 스레드에서 다른 스레드로에서 연결을 사용 하 고 세 번째 스레드에서 연결을 끊으라는 연결할 수 있습니다.  
  
 연결 풀에는 드라이버 관리자에서 유지 관리 됩니다. 응용 프로그램 호출 때 연결은 풀에서 선택 되어 **SQLConnect** 또는 **SQLDriverConnect** 응용 프로그램 호출 하는 경우 풀에 반환 되 고 **SQLDisconnect**. 풀의 크기는 요청 된 리소스 할당에 따라 동적으로 증가 합니다. 비활성 시간 제한에 따라 축소: 연결 (하지 사용 된 연결에서) 시간의 경과를 사용 하지 않으면, 풀에서 제거 됩니다. 풀의 크기는 메모리 제약 조건 및 서버에 대 한 제한에 의해서만 제한 됩니다.  
  
 드라이버 관리자에 전달 된 인수에 따라 풀에서 특정 연결을 사용할 것인지 여부를 결정 **SQLConnect** 또는 **SQLDriverConnect**, 연결 특성에 따라 연결 할당 된 후 설정 합니다.  
  
 드라이버 관리자는 연결 풀링 하는 경우 연결 전달 하기 전에 연결이 계속 작동 하는지 확인 하려면 필요 합니다. 그렇지 않으면 일시적인 네트워크 오류가 발생할 때마다 드라이버 관리자 응용 프로그램에 배달 못 한 연결 제한 전달에 유지 합니다. ODBC 3에는 새로운 연결 특성이 정의 되어*.x*: SQL_ATTR_CONNECTION_DEAD 합니다. SQL_CD_TRUE 또는 SQL_CD_FALSE를 반환 하는 읽기 전용 연결 특성입니다. 값 SQL_CD_TRUE SQL_CD_FALSE 즉, 연결이 아직 활성 상태인 동안 연결에 손실 된 것을 의미 합니다. (이전 버전의 ODBC에 맞는 드라이버가이 특성 지원할 수도 수 있습니다.)  
  
 드라이버를 효율적으로이 옵션을 구현 해야 하거나 연결 풀링 성능을 약화 됩니다. 특히,이 연결 속성을 가져오는 데 대 한 호출 서버 왕복을 발생 하지 않습니다. 대신, 드라이버는 연결의 마지막으로 알려진된 상태를 방금 반환 해야 합니다. 서버에 대 한 마지막 번 실패 한 경우 비활성 및 마지막 여행에 성공한 경우 데드 연결이 있습니다.  
  
## <a name="remarks"></a>주의  
 연결이 끊겼습니다 (SQL_ATTR_CONNECTION_DEAD를 통해 보고), ODBC 드라이버 관리자 SQLDisconnect 드라이버에서 호출 하 여 해당 연결을 삭제 됩니다. 새 연결 요청이 풀에서 사용 가능한 연결이 찾지 못할 수 있습니다. 결국 풀 빈 가정 하 고 새 연결을 드라이버 관리자 확인 될 수 있습니다.  
  
 연결 풀을 사용 하려면 응용 프로그램에서는 다음 단계를 수행 합니다.  
  
1.  호출 하 여 연결 풀링을 사용 하면 **SQLSetEnvAttr** SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_HENV로 SQL_ATTR_CONNECTION_POOLING 환경 특성을 설정 합니다. 이 호출 응용 프로그램에서 사용 하도록 설정 하는 연결에 대 한 풀링는 공유 환경 할당 되기 전에 수행 되어야 합니다. 환경 핸들에 대 한 호출에서 **SQLSetEnvAttr** SQL_ATTR_CONNECTION_POOLING 프로세스 수준 특성을 낮추는 null로 설정 해야 합니다. 특성이 SQL_CP_ONE_PER_DRIVER로 설정 된, 각 드라이버에 대해 단일 연결 풀을 사용할 수 있습니다. 일부 소수의 환경 많은 드라이버와 응용 프로그램 성공이 더 효율적일 수 있습니다 하므로 더 적은 비교 해야 할 수 있습니다. SQL_CP_ONE_PER_HENV, 단일 연결 풀으로 설정 각 환경에 대해 지원 됩니다. 다양 한 환경 및 몇 가지 드라이버와 응용 프로그램 성공이 더 효율적일 수 있습니다 하므로 더 적은 비교 해야 할 수 있습니다. 연결 풀링을 SQL_ATTR_CONNECTION_POOLING SQL_CP_OFF를 설정 하 여 사용할 수 없습니다.  
  
2.  호출 하 여 환경을 할당 **SQLAllocHandle** 와 *HandleType* 인수를 SQL_HANDLE_ENV로 설정 합니다. 이 호출에 의해 할당 되는 환경 연결 풀링을 설정 되어 있으므로 암시적 공유 환경이 됩니다. 그러나 사용할 환경 확인 되지 않으면까지 **SQLAllocHandle** 와 *HandleType* sql_handle_dbc 라는의이 환경에서 호출 됩니다.  
  
3.  연결을 호출 하 여 할당 **SQLAllocHandle** 와 *InputHandle* 를 SQL_HANDLE_DBC로 설정 및 *InputHandle* 에 할당 된 환경 핸들을 설정 합니다. 연결 풀링을 합니다. 드라이버 관리자는 응용 프로그램에서 설정 된 환경 특성과 일치 하는 기존 환경을 찾으려고 시도 합니다. 이러한 환경이 있는 경우 하나 만들어집니다 1 참조 카운트 (드라이버 관리자에서 유지). 일치 하는 공유 환경 발견 되 면 응용 프로그램에 반환 되는 환경 및 참조 개수가 증가 합니다. (사용 하 여 실제 연결 될 때까지 드라이버 관리자에서 확인 되지 않으면 **SQLConnect** 또는 **SQLDriverConnect** 호출 됩니다.)  
  
4.  호출 **SQLConnect** 또는 **SQLDriverConnect** 하 여 연결 합니다. 드라이버 관리자 연결 옵션에 대 한 호출에서 사용 하 여 **SQLConnect** (또는 연결 키워드에 대 한 호출에서 **SQLDriverConnect**) 연결 특성에 대 한 연결 할당 한 후 설정 사용 해야 하는 풀에서 연결을 확인 합니다.  
  
    > [!NOTE]  
    >  풀링된 연결에 요청 된 연결 일치 어떻게 SQL_ATTR_CP_MATCH 환경 특성에 의해 결정 됩니다. 자세한 내용은 참조 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)합니다.  
  
     ODBC 응용 프로그램 연결 풀링을 사용 하 여 호출 해야 [CoInitializeEx](http://go.microsoft.com/fwlink/?LinkID=116307) 응용 프로그램을 초기화 하는 동안 및 [CoUninitialize](http://go.microsoft.com/fwlink/?LinkId=116310) 응용 프로그램을 종료 합니다.  
  
5.  호출 **SQLDisconnect** 완료 한 후 연결 합니다. 연결이 연결 풀으로 반환 되 고 다시 사용 하기 위해 사용할 수 있게 됩니다.  
  
 심도 있는 논의 알려면 [Microsoft Data Access Components의 풀링](http://go.microsoft.com/fwlink/?LinkId=120776)합니다.  
  
## <a name="connection-pooling-considerations"></a>연결 풀링 고려 사항  
 SQL 명령을 사용 하 여 다음 작업 중 (아닌 ODBC API를 통해)를 수행 연결의 상태에 영향을 및 연결 풀링을 활성화 된 경우 예기치 않은 문제가 발생할 수 있습니다.  
  
-   연결을 열고 기본 데이터베이스를 변경 합니다.  
  
-   구성 가능한 옵션 (SET ROWCOUNT, ANSI_NULL, IMPLICIT_TRANSACTIONS, 실행 계획, 통계, TEXTSIZE, DATEFORMAT 및 포함)을 변경 하려면 SET 문을 사용 합니다.  
  
-   임시 테이블 및 저장된 프로시저를 만듭니다.  
  
 이러한 동작 중 하나는 ODBC API 밖에 서 수행, 이전 설정, 테이블 또는 프로시저 연결을 사용 하는 다음 사람이 자동으로 상속 합니다.  
  
> [!NOTE]  
>  연결 상태에 특정 설정이 필요 하지 않습니다. 항상 응용 프로그램의 연결 상태를 설정 하 고 응용 프로그램 설정을 풀링을 사용 하지 않는 모든 연결을 제거를 보장 해야 합니다.  
  
## <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링  
 Windows 8 부터는 ODBC 드라이버 연결을 사용할 수는 풀에 보다 효율적으로 합니다. 자세한 내용은 참조 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [연결에 대 한 데이터 원본이 나 드라이버](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [ODBC 드라이버를 개발합니다.](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft Data Access Components의 풀링](http://go.microsoft.com/fwlink/?LinkId=120776)
