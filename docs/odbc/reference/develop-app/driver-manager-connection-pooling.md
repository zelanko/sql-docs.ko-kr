---
title: 드라이버 관리자 연결 풀링 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 84ccc0db8f9a54eecc8337ca5efbc7b4c4baa239
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305824"
---
# <a name="driver-manager-connection-pooling"></a>드라이버 관리자 연결 풀링
연결 풀링을 사용 하면 응용 프로그램에서 각 사용을 위해 다시 설정 하지 않아도 되는 연결 풀의 연결을 사용할 수 있습니다. 연결이 만들어지고 풀에 배치 되 면 응용 프로그램은 전체 연결 프로세스를 수행 하지 않고 해당 연결을 다시 사용할 수 있습니다.  
  
 응용 프로그램에서 연결을 수행 하는 데 필요한 오버 헤드를 줄일 수 있으므로 풀링된 연결을 사용 하면 성능이 크게 향상 될 수 있습니다. 이는 네트워크를 통해 연결 하는 중간 계층 응용 프로그램 또는 인터넷 응용 프로그램과 같이 반복적으로 연결 하 고 연결을 끊는 응용 프로그램에 특히 중요할 수 있습니다.  
  
 연결 풀링 아키텍처를 사용 하면 성능 향상 외에도 단일 프로세스로 여러 구성 요소에서 환경과 연결 된 연결을 사용할 수 있습니다. 즉, 동일한 프로세스의 독립 실행형 구성 요소가 서로를 인식 하지 않고도 서로 상호 작용할 수 있습니다. 연결 풀의 연결은 여러 구성 요소에서 반복적으로 사용할 수 있습니다.  
  
> [!NOTE]
>  ODBC 2를 사용 하는 ODBC 응용 프로그램에서 연결 풀링을 사용할 수 있습니다. *x* 동작은 응용 프로그램이 *SQLSetEnvAttr*를 호출할 수 있는 경우에만 가능 합니다. 연결 풀링을 사용 하는 경우 응용 프로그램은 데이터베이스 \< *이름을* 변경 하는 것과 같이 데이터베이스 또는 데이터베이스의 컨텍스트를 변경 하는 SQL 문을 실행 하지 않아야 합니다. 그러면 데이터 원본에서 사용 하는 카탈로그를 변경 하는>.  


 ODBC 드라이버는 완전히 스레드로부터 안전 해야 하며 연결 풀링을 지원 하기 위해 연결에 스레드 선호도가 없어야 합니다. 즉, 드라이버는 언제 든 지 모든 스레드에 대 한 호출을 처리할 수 있으며 한 스레드에서 연결 하 여 다른 스레드에서 연결을 사용 하 고 세 번째 스레드에서 연결을 끊을 수 있습니다.  
  
 연결 풀은 드라이버 관리자에 의해 유지 관리 됩니다. 응용 프로그램에서 **SQLConnect** 또는 **SQLDriverConnect** 를 호출할 때 풀에서 연결을 그리면 응용 프로그램이 **sqldisconnect**를 호출할 때 풀로 반환 됩니다. 풀의 크기는 요청 된 리소스 할당에 따라 동적으로 증가 합니다. 비활성 시간 제한에 따라 축소: 연결이 일정 시간 동안 비활성 상태인 경우 (연결에서 사용 되지 않음) 풀에서 제거 됩니다. 풀 크기는 서버에 대 한 메모리 제약 조건 및 제한에 의해서만 제한 됩니다.  
  
 드라이버 관리자는 **SQLConnect** 또는 **SQLDriverConnect**에 전달 된 인수에 따라 그리고 연결이 할당 된 후 설정 된 연결 특성에 따라 풀의 특정 연결을 사용할지 여부를 결정 합니다.  
  
 드라이버 관리자가 연결을 풀링 하는 경우 연결을 처리 하기 전에 연결을 계속 사용 하 고 있는지 확인할 수 있어야 합니다. 그렇지 않으면 드라이버 관리자는 일시적인 네트워크 오류가 발생할 때마다 응용 프로그램에 대 한 중단 된 연결을 유지 합니다. ODBC 3.x에 새 연결 특성이 정의 되어 있습니다.*x*: SQL_ATTR_CONNECTION_DEAD. SQL_CD_TRUE 또는 SQL_CD_FALSE를 반환 하는 읽기 전용 연결 특성입니다. 값 SQL_CD_TRUE는 연결이 끊어진 것을 의미 하 고, 값 SQL_CD_FALSE는 연결이 아직 활성 상태인 것을 의미 합니다. 이전 버전의 ODBC를 준수 하는 드라이버도이 특성을 지원할 수 있습니다.  
  
 드라이버는이 옵션을 효율적으로 구현 해야 합니다. 그렇지 않으면 연결 풀링 성능이 저하 됩니다. 특히이 연결 특성을 가져오기 위해 호출 하면 서버로의 라운드트립이 발생 하지 않습니다. 대신 드라이버는 마지막으로 알려진 연결 상태를 반환 해야 합니다. 서버에 대 한 마지막 이동이 실패 한 경우 연결이 중단 되 고 마지막으로 성공한 경우에는 작동 하지 않습니다.  
  
## <a name="remarks"></a>설명  
 연결이 끊어진 경우 (SQL_ATTR_CONNECTION_DEAD을 통해 보고) ODBC 드라이버 관리자는 드라이버에서 SQLDisconnect를 호출 하 여 해당 연결을 제거 합니다. 새 연결 요청이 풀에서 사용할 수 있는 연결을 찾을 수 없습니다. 결과적으로, 풀이 비어 있는 경우 드라이버 관리자가 새 연결을 만들 수 있습니다.  
  
 연결 풀을 사용 하기 위해 응용 프로그램에서는 다음 단계를 수행 합니다.  
  
1.  **SQLSetEnvAttr** 를 호출 하 여 SQL_ATTR_CONNECTION_POOLING 환경 특성을 SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_HENV으로 설정 하 여 연결 풀링을 사용 하도록 설정 합니다. 응용 프로그램에서 연결 풀링을 사용 하도록 설정할 공유 환경을 할당 하기 전에이 호출을 수행 해야 합니다. **SQLSetEnvAttr** 에 대 한 호출의 환경 핸들은 null로 설정 해야 합니다. 그러면 프로세스 수준 특성을 SQL_ATTR_CONNECTION_POOLING 합니다. 특성이 SQL_CP_ONE_PER_DRIVER로 설정 된 경우 각 드라이버에 대해 단일 연결 풀이 지원 됩니다. 응용 프로그램이 많은 드라이버와 소수의 환경에서 작동 하는 경우 더 적은 비교가 필요할 수 있으므로 더 효율적일 수 있습니다. SQL_CP_ONE_PER_HENV로 설정 된 경우 각 환경에 대해 단일 연결 풀이 지원 됩니다. 응용 프로그램이 여러 환경과 몇 개의 드라이버에서 작동 하는 경우 더 적은 비교가 필요할 수 있으므로 더 효율적일 수 있습니다. SQL_ATTR_CONNECTION_POOLING을 SQL_CP_OFF 설정 하 여 연결 풀링을 사용 하지 않도록 설정 합니다.  
  
2.  *HandleType* 인수가 SQL_HANDLE_ENV로 설정 된 **SQLAllocHandle** 를 호출 하 여 환경을 할당 합니다. 연결 풀링이 사용 하도록 설정 되었기 때문에이 호출에서 할당 한 환경은 암시적 공유 환경이 됩니다. 그러나 사용할 환경은이 환경에서 SQL_HANDLE_DBC *HandleType* 의 **SQLAllocHandle** 가 호출 될 때까지 결정 되지 않습니다.  
  
3.  *InputHandle* 가 SQL_HANDLE_DBC로 설정 되 고 *InputHandle* 가 연결 풀링을 위해 할당 된 환경 핸들로 설정 된 **SQLAllocHandle** 를 호출 하 여 연결을 할당 합니다. 드라이버 관리자는 응용 프로그램에서 설정한 환경 특성과 일치 하는 기존 환경을 찾으려고 시도 합니다. 이러한 환경이 없으면 1의 참조 횟수 (드라이버 관리자에서 유지 관리)를 사용 하 여 하나를 만듭니다. 일치 하는 공유 환경이 발견 되 면 환경이 응용 프로그램에 반환 되 고 참조 횟수가 증가 합니다. **SQLConnect** 또는 **SQLDriverConnect** 를 호출할 때까지 사용 되는 실제 연결은 드라이버 관리자에 의해 결정 되지 않습니다.  
  
4.  **SQLConnect** 또는 **SQLDriverConnect** 를 호출 하 여 연결을 설정 합니다. 드라이버 관리자는 **SQLConnect** 에 대 한 호출 (또는 **SQLDriverConnect**에 대 한 호출의 연결 키워드)의 연결 옵션을 사용 하 고 연결 할당 후에 설정 된 연결 특성을 사용 하 여 풀에서 사용할 연결을 결정 합니다.  
  
    > [!NOTE]  
    >  요청 된 연결이 풀링된 연결과 일치 하는 방법은 SQL_ATTR_CP_MATCH 환경 특성에 의해 결정 됩니다. 자세한 내용은 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)를 참조 하세요.  
  
     연결 풀링을 사용 하는 ODBC 응용 프로그램은 응용 프로그램을 초기화 하는 동안 [CoInitializeEx](https://go.microsoft.com/fwlink/?LinkID=116307) [를 호출](https://go.microsoft.com/fwlink/?LinkId=116310) 해야 합니다.  
  
5.  연결이 완료 되 면 **Sqldisconnect** 를 호출 합니다. 연결이 연결 풀로 반환 되 고 다시 사용할 수 있게 됩니다.  
  
 자세한 내용은 [Microsoft Data Access 구성 요소에서 풀링](https://go.microsoft.com/fwlink/?LinkId=120776)을 참조 하세요.  
  
## <a name="connection-pooling-considerations"></a>연결 풀링 고려 사항  
 ODBC API를 통하지 않고 SQL 명령을 사용 하 여 다음 작업을 수행 하면 연결 상태에 영향을 줄 수 있으며 연결 풀링이 활성화 되어 있을 때 예기치 않은 문제가 발생할 수 있습니다.  
  
-   연결을 열고 기본 데이터베이스를 변경 합니다.  
  
-   SET 문을 사용 하 여 SET ROWCOUNT, ANSI_NULL, IMPLICIT_TRANSACTIONS, 실행 계획, 통계, TEXTSIZE, DATEFORMAT 등의 구성 가능한 옵션을 변경할 수 있습니다.  
  
-   임시 테이블 및 저장 프로시저 만들기  
  
 ODBC API 외부에서 이러한 작업을 수행 하는 경우에는 연결을 사용 하는 다음 사용자가 자동으로 이전 설정, 테이블 또는 프로시저를 상속 합니다.  
  
> [!NOTE]  
>  연결 상태에 특정 설정이 표시 되지 않을 것으로 간주 합니다. 응용 프로그램에서 항상 연결 상태를 설정 하 고 사용 하지 않는 연결 풀링 설정을 응용 프로그램에서 제거 하는지 확인 해야 합니다.  
  
## <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링  
 Windows 8부터 ODBC 드라이버는 풀의 연결을 보다 효율적으로 사용할 수 있습니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 원본 또는 드라이버에 연결](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 데이터 액세스 구성 요소의 풀링](https://go.microsoft.com/fwlink/?LinkId=120776)
