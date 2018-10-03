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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e03932fe9d6cc98648c2e0da2e2cdd963a8d67f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826141"
---
# <a name="driver-manager-connection-pooling"></a>드라이버 관리자 연결 풀링
연결 풀링은 응용 프로그램을 다시 사용할 때마다 설정할 필요가 없는 연결 풀에서 연결을 사용 합니다. 연결 생성 되었으며 풀에 배치 되 면 응용 프로그램 전체 연결 프로세스를 수행 하지 않고 해당 연결 다시 사용할 수 있습니다.  
  
 풀링된 연결을 사용 하 여 응용 프로그램을 연결 하는 중에 관련 된 오버 헤드를 줄일 수 때문에 성능이 크게 향상 될 수 있습니다. 이 네트워크를 통해 연결 하는 중간 계층 응용 프로그램 또는 반복적으로 연결 하 고 연결 끊기, 인터넷 응용 프로그램과 같은 응용 프로그램에 특히 중요할 수 있습니다.  
  
 성능 향상 외에도 연결 풀링 아키텍처 environment 및 해당 관련된 연결이 단일 프로세스에서 여러 구성 요소에서 사용할 수 있습니다. 이 서로 인식 하지 않고 동일한 프로세스에서 독립 실행형 구성 요소가 서로 상호 작용할 수 있음을 의미 합니다. 여러 구성 요소에서 연결 풀에서 연결을 반복적으로 사용할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 2를 표시 하는 ODBC 응용 프로그램에서 연결 풀링을 사용할 수 있습니다. *x* 동작을 응용 프로그램에서 호출할 수 만큼 *SQLSetEnvAttr*합니다. 응용 프로그램 연결 풀링을 사용 하는 경우 데이터베이스 또는 데이터베이스를 변경 하는 등의 컨텍스트를 변경 하는 SQL 문을 실행 해서는 안 합니다 \< *데이터베이스 * * 이름*>, 카탈로그에서 사용 하는 변경 내용을 데이터 원본입니다.  
  
 ODBC 드라이버는 완벽 하 게 스레드로부터 안전 해야 하며 연결에는 연결 풀링을 지원 하기 위해 스레드 선호도 없어야 합니다. 즉, 드라이버는 언제 든 지 모든 스레드에서 호출을 처리 하 고 스레드와 다른 스레드에서 연결을 사용 하 고 세 번째 스레드에서 연결 끊기에 연결할 수 있습니다.  
  
 연결 풀에는 드라이버 관리자에 의해 유지 관리 됩니다. 응용 프로그램을 호출할 때 연결 풀에서 가져온 **SQLConnect** 하거나 **SQLDriverConnect** 응용 프로그램을 호출 하는 경우 풀에 반환 되 고 **SQLDisconnect**. 풀의 크기는 요청 된 리소스 할당에 따라 동적으로 증가 합니다. 비활성 시간에 따라 축소: (이 사용 되지 않은 연결에서) 기간에 대 한 연결이 활성화 되지 풀에서 제거 됩니다. 풀의 크기는 메모리 제약 조건 및 서버에 대 한 제한에 의해서만 제한 됩니다.  
  
 드라이버 관리자에 전달 된 인수에 따라 풀의 특정 연결을 사용할 것인지 여부를 결정 **SQLConnect** 하거나 **SQLDriverConnect**, 및 연결 특성에 따라 연결 할당 된 후 설정 합니다.  
  
 드라이버 관리자 연결 풀링는, 하는 경우 연결 전달 하기 전에 연결을 여전히 작동 하는지 확인할 수 해야 합니다. 이 고, 그렇지 일시적인 네트워크 오류가 발생할 때마다 드라이버 관리자 응용 프로그램에 데드 연결 제한 처리에 유지 합니다. ODBC 3에서 새로운 연결 특성을 정의한 *.x*: SQL_ATTR_CONNECTION_DEAD 합니다. SQL_CD_TRUE 또는 SQL_CD_FALSE를 반환 하는 읽기 전용 연결 특성입니다. 값 SQL_CD_TRUE SQL_CD_FALSE 값 연결이 여전히 활성 상태 인지를 의미 하는 동안 연결에 손실 된 것을 의미 합니다. (이전 버전의 ODBC에 맞는 드라이버가이 특성 지원할 수도 수 있습니다.)  
  
 드라이버는이 옵션을 효율적으로 구현 해야 합니다 또는 성능 풀링 연결을 약화 됩니다. 특히,이 연결 특성을 가져오기 위한 호출 하면 서버에 왕복 합니다. 대신, 드라이버 연결의 마지막으로 알려진된 상태를 바로 반환 해야 합니다. 연결이 마지막 여정 서버로 실패 한 경우 중지 및 마지막 여정에 성공한 경우 소멸 됩니다.  
  
## <a name="remarks"></a>Remarks  
 연결이 끊어졌습니다 (SQL_ATTR_CONNECTION_DEAD를 통해 보고 됨), ODBC 드라이버 관리자는 SQLDisconnect 드라이버에서 호출 하 여 해당 연결을 삭제 됩니다. 새 연결 요청이 풀에서 사용 가능한 연결이 찾지 못할 수 있습니다. 결국 풀 비어 가정 하 고 새 연결을 드라이버 관리자 확인 될 수 있습니다.  
  
 연결 풀을 사용 하려면 응용 프로그램에는 다음 단계를 수행 합니다.  
  
1.  호출 하 여 연결 풀링을 사용 하도록 설정 **SQLSetEnvAttr** SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_HENV로 SQL_ATTR_CONNECTION_POOLING 환경 특성을 설정 합니다. 이 호출은 응용 프로그램은 연결 풀링이 사용 하도록 설정 하는 공유 환경에서 할당 전에 수행 되어야 합니다. 호출에서 환경 핸들 **SQLSetEnvAttr** SQL_ATTR_CONNECTION_POOLING 프로세스 수준 특성을 사용 하면 null로 설정 해야 합니다. 특성 SQL_CP_ONE_PER_DRIVER로 각 드라이버에 대 한 단일 연결 풀을 사용할 수 있습니다. 응용 프로그램 몇 가지 환경과 많은 드라이버를 사용 하 여 작동 하는 경우이 더 효율적일 수 있습니다 되므로 적은 비교 해야 할 수 있습니다. SQL_CP_ONE_PER_HENV, 단일 연결 풀으로 각 환경에 대해 지원 되 면 다양 한 환경 및 몇 가지 드라이버를 사용 하 여 응용 프로그램 작동 하는 경우이 더 효율적일 수 있습니다 되므로 적은 비교 해야 할 수 있습니다. SQL_ATTR_CONNECTION_POOLING SQL_CP_OFF을 설정 하 여 연결 풀링 비활성화 됩니다.  
  
2.  호출 하 여 환경을 할당 **SQLAllocHandle** 사용 하 여 합니다 *HandleType* 인수를 SQL_HANDLE_ENV로 설정 합니다. 이 호출에 의해 할당 되는 환경 연결 풀링을 설정 되어 있기 때문에 암시적 공유 environment이 됩니다. 하지만 사용할 환경을 결정 되지 않습니다까지 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DBC의는이 환경에서 호출 됩니다.  
  
3.  호출 하 여 연결을 할당 **SQLAllocHandle** 사용 하 여 *InputHandle* 를 SQL_HANDLE_DBC로 설정 하 고 *InputHandle* 에 할당 된 환경 핸들을로 설정 연결 풀링 드라이버 관리자는 응용 프로그램이 설정한 환경 특성과 일치 하는 기존 환경을 찾으려고 시도 합니다. 이러한 환경이 있는 경우 하나 만들어집니다 1 참조 카운트 (드라이버 관리자에 의해 유지 관리 됨). 일치 하는 공유 환경 있으면 환경 응용 프로그램에 반환 됩니다 하 고 해당 참조 개수가 증가 합니다. (사용 하는 실제 연결 될 때까지 드라이버 관리자에 의해 결정 되지 않습니다 **SQLConnect** 하거나 **SQLDriverConnect** 라고 합니다.)  
  
4.  호출 **SQLConnect** 하거나 **SQLDriverConnect** 연결 합니다. 드라이버 관리자 연결 옵션을 사용 하 여 호출에서 **SQLConnect** (또는 연결 키워드에 대 한 호출에 **SQLDriverConnect**) 연결 특성에 연결을 할당 한 후 설정 풀에서 연결을 사용할지를 결정 합니다.  
  
    > [!NOTE]  
    >  풀링된 연결으로 요청 된 연결을 일치 하는 방법을 SQL_ATTR_CP_MATCH 환경 특성에 의해 결정 됩니다. 자세한 내용은 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)합니다.  
  
     ODBC 응용 프로그램은 연결 풀링을 사용 하 여 호출 해야 [CoInitializeEx](http://go.microsoft.com/fwlink/?LinkID=116307) 응용 프로그램을 초기화 하는 동안 및 [CoUninitialize](http://go.microsoft.com/fwlink/?LinkId=116310) 응용 프로그램을 닫을 때.  
  
5.  호출 **SQLDisconnect** 연결 작업을 완료 합니다. 연결이 연결 풀으로 반환 되 고 다시 사용 하기 위해 사용할 수 있게 됩니다.  
  
 자세한 내용은 참조 하세요. [Microsoft Data Access Components의 풀링](http://go.microsoft.com/fwlink/?LinkId=120776)합니다.  
  
## <a name="connection-pooling-considerations"></a>연결 풀링 고려 사항  
 SQL 명령을 사용 하 여 다음 작업 중 (대신 ODBC API를 통해) 수행 연결의 상태에 영향을 하 고 연결 풀링이 활성화 되어 있을 때 예기치 않은 문제가 발생할 수 있습니다.  
  
-   연결을 열고 기본 데이터베이스를 변경 합니다.  
  
-   SET ROWCOUNT, ANSI_NULL, IMPLICIT_TRANSACTIONS, 실행 계획, 통계, TEXTSIZE를 및 DATEFORMAT 등 구성 가능한 옵션을 변경 하려면 SET 문을 사용 합니다.  
  
-   임시 테이블 및 저장된 프로시저를 만드는 중입니다.  
  
 이러한 작업을 수행 하는 ODBC API를 외부에서 이전 설정, 테이블 또는 프로시저 연결을 사용 하는 다음 사람이 자동으로 상속 됩니다.  
  
> [!NOTE]  
>  연결 상태에 특정 설정을 기다리지는 않습니다. 항상 응용 프로그램에서 연결 상태를 설정 하 고 응용 프로그램 설정을 풀링을 사용 하지 않는 연결을 제거 함을 확인 해야 합니다.  
  
## <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링  
 Windows 8부터 ODBC 드라이버에서에서 사용할 수 연결 풀을 보다 효율적으로. 자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [연결에 대 한 데이터 원본 또는 드라이버](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft Data Access Components의 풀링](http://go.microsoft.com/fwlink/?LinkId=120776)
