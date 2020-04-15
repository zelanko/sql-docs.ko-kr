---
title: 드라이버 관리자 연결 풀링 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305824"
---
# <a name="driver-manager-connection-pooling"></a>드라이버 관리자 연결 풀링
연결 풀링을 사용하면 응용 프로그램에서 각 용도에 대해 다시 설정할 필요가 없는 연결 풀의 연결을 사용할 수 있습니다. 연결이 만들어지고 풀에 배치되면 응용 프로그램은 전체 연결 프로세스를 수행하지 않고 해당 연결을 다시 사용할 수 있습니다.  
  
 풀린 연결을 사용하면 응용 프로그램이 연결에 관련된 오버헤드를 절약할 수 있으므로 상당한 성능 향상을 초래할 수 있습니다. 이는 네트워크를 통해 연결되는 중간 계층 응용 프로그램이나 인터넷 응용 프로그램과 같이 반복적으로 연결하고 연결을 끊는 응용 프로그램에 특히 중요할 수 있습니다.  
  
 연결 풀링 아키텍처를 사용하면 성능 향상 외에도 단일 프로세스에서 여러 구성 요소에서 환경 및 관련 연결을 사용할 수 있습니다. 즉, 동일한 프로세스의 독립 실행형 구성 요소는 서로를 인식하지 않고 서로 상호 작용할 수 있습니다. 연결 풀의 연결은 여러 구성 요소에서 반복적으로 사용할 수 있습니다.  
  
> [!NOTE]
>  연결 풀링은 ODBC 2를 나타내는 ODBC 응용 프로그램에서 사용할 수 있습니다. *응용* 프로그램이 *SQLSetEnvAttr을*호출할 수 있는 한 x 동작 . 연결 풀링을 사용하는 경우 응용 프로그램은 데이터베이스 또는 데이터베이스 컨텍스트를 변경하는 SQL 문을 \<실행하지 않아야 합니다(예: *데이터베이스 이름*> 변경, 데이터 원본에서 사용하는 카탈로그 변경)  


 ODBC 드라이버는 완전히 스레드 가 용이해야 하며 연결풀링을 지원하기 위해 스레드 선호도가 없어야 합니다. 즉, 드라이버는 언제든지 모든 스레드에서 호출을 처리할 수 있으며 한 스레드에 연결하고, 다른 스레드에서 연결을 사용하고, 세 번째 스레드에서 연결을 끊을 수 있습니다.  
  
 연결 풀은 드라이버 관리자에 의해 유지 관리됩니다. 연결은 응용 프로그램이 **SQLConnect** 또는 **SQLDriverConnect를** 호출할 때 풀에서 그려지고 응용 프로그램이 **SQLDisconnect**를 호출할 때 풀로 반환됩니다. 풀의 크기는 요청된 리소스 할당에 따라 동적으로 증가합니다. 비활성 시간 초과에 따라 축소: 연결이 시간 동안 비활성 상태인 경우(연결에서 사용되지 않음) 풀에서 제거됩니다. 풀의 크기는 서버의 메모리 제약 조건과 제한에 의해서만 제한됩니다.  
  
 드라이버 관리자는 **SQLConnect** 또는 **SQLDriverConnect에서**전달된 인수에 따라 풀의 특정 연결을 사용할지 여부와 연결이 할당된 후 설정된 연결 특성에 따라 사용할지 여부를 결정합니다.  
  
 드라이버 관리자가 연결을 풀링하는 경우 연결을 전달하기 전에 연결이 여전히 작동하는지 확인할 수 있어야 합니다. 그렇지 않으면 일시적인 네트워크 오류가 발생할 때마다 드라이버 관리자는 응용 프로그램에 대한 데드 연결을 계속 전달합니다. 새 연결 특성은 ODBC 3 *.x*: SQL_ATTR_CONNECTION_DEAD 정의되었습니다. 이 SQL_CD_TRUE 또는 SQL_CD_FALSE 반환하는 읽기 전용 연결 특성입니다. SQL_CD_TRUE 값은 연결이 손실되었음을 의미하지만 SQL_CD_FALSE 값은 연결이 여전히 활성 상태임을 의미합니다. (ODBC의 이전 버전을 준수하는 드라이버도 이 특성을 지원할 수 있습니다.)  
  
 드라이버는 이 옵션을 효율적으로 구현해야 하거나 연결 풀링 성능이 저하됩니다. 특히 이 연결 특성을 얻기 위한 호출은 서버에 왕복을 일으키지 않아야 합니다. 대신 드라이버는 마지막으로 알려진 연결 상태를 반환해야 합니다. 서버에 대한 마지막 트립이 실패한 경우 연결이 끊어지고 마지막 트립이 성공하면 죽지 않습니다.  
  
## <a name="remarks"></a>설명  
 연결이 끊어진 경우(SQL_ATTR_CONNECTION_DEAD 통해 보고됨) ODBC 드라이버 관리자는 드라이버에서 SQLDisconnect를 호출하여 해당 연결을 삭제합니다. 새 연결 요청이 풀에서 사용 가능한 연결을 찾지 못할 수 있습니다. 결국 드라이버 관리자는 풀이 비어 있다고 가정하여 새 연결을 만들 수 있습니다.  
  
 연결 풀을 사용하려면 응용 프로그램이 다음 단계를 수행합니다.  
  
1.  **SQLSetEnvAttr을** 호출하여 연결 풀링을 활성화하여 SQL_ATTR_CONNECTION_POOLING 환경 특성을 SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_HENV 설정합니다. 응용 프로그램에서 연결 풀링을 사용하도록 설정할 공유 환경을 할당하기 전에 이 호출을 수행해야 합니다. **SQLSetEnvAttr에** 대 한 호출에서 환경 핸들 null로 설정 해야 합니다., SQL_ATTR_CONNECTION_POOLING 프로세스 수준 특성을 만듭니다. 특성이 SQL_CP_ONE_PER_DRIVER 설정된 경우 각 드라이버에 대해 단일 연결 풀이 지원됩니다. 응용 프로그램이 많은 드라이버와 몇 가지 환경에서 작동하는 경우 비교횟수가 적을 수 있으므로 더 효율적일 수 있습니다. SQL_CP_ONE_PER_HENV 설정하면 각 환경에 대해 단일 연결 풀이 지원됩니다. 응용 프로그램이 많은 환경과 적은 드라이버에서 작동하는 경우 비교횟수가 적을 수 있으므로 더 효율적일 수 있습니다. SQL_CP_OFF SQL_ATTR_CONNECTION_POOLING 설정하여 연결 풀링을 사용할 수 없습니다.  
  
2.  SQL_HANDLE_ENV 설정된 *HandleType* 인수를 사용하여 **SQLAllocHandle을** 호출하여 환경을 할당합니다. 연결 풀링이 활성화되었기 때문에 이 호출에서 할당된 환경은 암시적 공유 환경이 됩니다. 그러나 *핸들 유형SQL_HANDLE_DBC* 을 사용하는 **SQLAllocHandle이** 이 환경에서 호출될 때까지 사용할 환경은 결정되지 않습니다.  
  
3.  *SQL_HANDLE_DBC* 설정 된 **inputAllocHandle을** 호출 하 여 연결을 할당 하 고 *입력 핸들* 연결 풀링에 할당 된 환경 핸들에 설정 합니다. 드라이버 관리자는 응용 프로그램에서 설정한 환경 특성과 일치하는 기존 환경을 찾으려고 시도합니다. 이러한 환경이 없으면 1의 참조 개수(드라이버 관리자가 유지 관리)를 통해 환경이 만들어집니다. 일치하는 공유 환경이 발견되면 환경이 응용 프로그램에 반환되고 참조 수가 증가합니다. (사용할 실제 연결은 **SQLConnect** 또는 **SQLDriverConnect가** 호출될 때까지 드라이버 관리자에 의해 결정되지 않습니다.)  
  
4.  연결을 위해 **SQLConnect** 또는 **SQLDriverConnect를** 호출합니다. 드라이버 관리자는 **SQLConnect** 호출의 연결 옵션(또는 **SQLDriverConnect**호출의 연결 키워드)과 연결 할당 후 설정된 연결 특성을 사용하여 풀에서 사용할 연결을 결정합니다.  
  
    > [!NOTE]  
    >  요청된 연결이 풀려진 연결과 일치하는 방법은 SQL_ATTR_CP_MATCH 환경 특성에 의해 결정됩니다. 자세한 내용은 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)을 참조하십시오.  
  
     연결 풀링을 사용하는 ODBC 응용 프로그램은 응용 프로그램 초기화 중에 [CoInitializeEx를](https://go.microsoft.com/fwlink/?LinkID=116307) 호출하고 응용 프로그램이 닫히면 [CoUninitialize를](https://go.microsoft.com/fwlink/?LinkId=116310) 호출해야 합니다.  
  
5.  연결이 완료되면 **SQLDisconnect를** 호출합니다. 연결이 연결 풀로 반환되고 다시 사용할 수 있게 됩니다.  
  
 자세한 내용은 Microsoft 데이터 [액세스 구성 요소의 풀링을](https://go.microsoft.com/fwlink/?LinkId=120776)참조하십시오.  
  
## <a name="connection-pooling-considerations"></a>연결 풀링 고려 사항  
 ODBC API가 아닌 SQL 명령을 사용하여 다음 작업을 수행하면 연결 상태에 영향을 미치고 연결 풀링이 활성화된 경우 예기치 않은 문제가 발생할 수 있습니다.  
  
-   연결을 열고 기본 데이터베이스를 변경합니다.  
  
-   SET 문을 사용하여 구성 가능한 옵션(설정 행 계산, ANSI_NULL, IMPLICIT_TRANSACTIONS, SHOWPLAN, 통계, TEXTSIZE 및 DATEFORMAT 포함)을 변경합니다.  
  
-   임시 테이블 및 저장 프로시저 만들기  
  
 이러한 작업이 ODBC API 외부에서 수행되는 경우 연결을 사용하는 다음 사용자는 자동으로 이전 설정, 테이블 또는 프로시저를 상속합니다.  
  
> [!NOTE]  
>  연결 상태에 특정 설정이 있을 것으로 예상하지 마십시오. 항상 응용 프로그램의 연결 상태를 설정하고 응용 프로그램이 사용되지 않는 연결 풀링 설정을 제거해야 합니다.  
  
## <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링  
 Windows 8부터 ODBC 드라이버는 풀에서 연결을 보다 효율적으로 사용할 수 있습니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 원본 또는 드라이버에 연결](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 데이터 액세스 구성 요소의 풀링](https://go.microsoft.com/fwlink/?LinkId=120776)
