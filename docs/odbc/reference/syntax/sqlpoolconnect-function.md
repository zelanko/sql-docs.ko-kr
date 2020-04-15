---
title: SQLPoolConnect 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5045fe47683529f858b01e69f6af696e2821ca4c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306904"
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect Function
**규칙**  
 버전 출시: ODBC 3.8 표준 규정 준수: ODBC  
  
 **요약**  
 **SQLPoolConnect는** 풀에서 연결을 다시 사용할 수 없는 경우 새 연결을 만드는 데 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>인수  
 *hDbc*  
 [입력] 연결 핸들입니다.  
  
 *hDbcInfo토큰*  
 [입력] 새 응용 프로그램 연결 요청에 대한 토큰 핸들입니다.  
  
 *wszOut커넥트스트링*  
 [출력] 완료된 연결 문자열에 대한 버퍼에 대한 포인터입니다. 대상 데이터 원본에 성공적으로 연결하면 이 버퍼에는 완료된 연결 문자열이 포함됩니다. 응용 프로그램은 이 버퍼에 대해 최소 1,024자를 할당해야 합니다.  
  
 *wszOutConnectString이* NULL인 경우 *cchConnectStringLen은* *wszOutConnectString이*가리키는 버퍼에서 반환할 수 있는 총 문자 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *cch커넥트스트링버퍼*  
 [입력] **wszOutConnectString* 버퍼의 길이입니다.  
  
 *cch커넥트스트링렌*  
 [출력] \* *wszOutConnectString에서*반환할 수 있는 총 문자 수(null-termination 문자 제외)를 반환하는 버퍼에 대한 포인터입니다. 반환할 수 있는 문자 수가 *cchConnectStringBuffer보다*크거나 같으면 \* *wszOutConnectString의* 완료된 연결 문자열이 *cchConnectStringBuffer에서* null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 드라이버 관리자가 **핸들 SQL_HANDLE_DBC_INFO_TOKEN** *및 hDbcInfoToken* **핸들을** 사용 한다는 점을 제외 하 고 입력 유효성 검사 오류에 대 한 [SQLDriverConnect와](../../../odbc/reference/syntax/sqldriverconnect-function.md) 비슷합니다.  
  
## <a name="remarks"></a>설명  
 드라이버 관리자는 hDbc 및 *hDbcInfoToken의* 상위 HENV 핸들이 동일하다는 것을 보장합니다. *hDbc*  
  
 [SQLDriverConnect와](../../../odbc/reference/syntax/sqldriverconnect-function.md)달리 사용자에게 연결 정보를 입력하라는 메시지를 표시하는 *드라이버완성* 인수가 없습니다. 풀링 시나리오에서는 프롬프트 대화 상자가 허용되지 않습니다.  
  
 응용 프로그램은 이 함수를 직접 호출해서는 안 됩니다. 드라이버 인식 연결 풀링을 지원하는 ODBC 드라이버는 이 기능을 구현해야 합니다.  
  
 드라이버가 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환할 때마다 드라이버 관리자는 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 또는 [SQLDriverConnect에서](../../../odbc/reference/syntax/sqldriverconnect-function.md)응용 프로그램에 오류를 반환합니다.  
  
 드라이버가 SQL_SUCCESS_WITH_INFO 반환할 때마다 드라이버 관리자는 *hDbcInfoToken에서*진단 정보를 얻고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 및 [SQLDriverConnect에서](../../../odbc/reference/syntax/sqldriverconnect-function.md)응용 프로그램에 SQL_SUCCESS_WITH_INFO 반환합니다.  
  
 응용 프로그램에서 [SQLConnect를](../../../odbc/reference/syntax/sqlconnect-function.md)사용하는 경우 *wszOutConnectString은* NULL 버퍼가 됩니다(마지막 세 매개 변수는 모두 NULL, 0, NULL로 설정됩니다). 그렇지 않으면 드라이버는 응용 프로그램의 [SQLDriverConnect Function](../../../odbc/reference/syntax/sqldriverconnect-function.md) 호출로 반환되는 출력 연결 문자열을 반환해야 합니다.  
  
 ODBC 드라이버 개발을 위해 sqlspi.h를 포함합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
