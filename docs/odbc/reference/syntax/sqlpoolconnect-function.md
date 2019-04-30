---
title: SQLPoolConnect 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4dda69fa741555f4402bded930f68260b154fd30
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262256"
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect Function
**규칙**  
 도입 된 버전: ODBC 3.8 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLPoolConnect** 풀에서 연결을 다시 사용할 수 있으면 새 연결을 만드는 데 사용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
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
  
 *hDbcInfoToken*  
 [입력] 새 응용 프로그램 연결 요청 토큰 핸들입니다.  
  
 *wszOutConnectString*  
 [출력] 완료 된 연결 문자열에 대 한 버퍼에 대 한 포인터입니다. 연결에 성공 하면 대상 데이터 원본에이 버퍼는 완료 된 연결 문자열을 포함합니다. 응용 프로그램에는이 버퍼에 대 한 최소 1,024 자 할당 해야 합니다.  
  
 하는 경우 *wszOutConnectString* 가 null 인 경우 *cchConnectStringLen* (문자 데이터에 대 한 null 종료 문자를 제외한) 문자의 총 수를 반환 계속 됩니다에서 반환할 수는 가리키는 버퍼 *wszOutConnectString*합니다.  
  
 *cchConnectStringBuffer*  
 [입력] 길이 **wszOutConnectString* 문자에서 버퍼입니다.  
  
 *cchConnectStringLen*  
 [출력] 문자 (null 종결 문자가 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *wszOutConnectString*합니다. 반환할 사용 가능한 문자 개수 보다 크거나 같은 경우 *cchConnectStringBuffer*의 연결 문자열에서 완료 \* *wszOutConnectString* 잘립니다*cchConnectStringBuffer* null 종료 문자 길이 뺀 값입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO를 SQL_ERROR, 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 비슷합니다 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 드라이버 관리자를 사용 한다는 점을 제외 하면 모든 입력 유효성 검사 오류에 대 한를 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN의와 **처리** 의 *hDbcInfoToken*합니다.  
  
## <a name="remarks"></a>Remarks  
 드라이버 관리자 부모 HENV 처리 보장 *hDbc* 하 고 *hDbcInfoToken* 동일 합니다.  
  
 달리 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md), 방법이 없습니다 *DriverCompletion* 인수 연결 정보를 입력 하 라는 메시지가 표시 됩니다. 묻는 대화 상자가 풀링 시나리오에서 허용 되지 않습니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 드라이버는 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환 될 때마다 응용 프로그램에 드라이버 관리자 오류를 반환 합니다 (에서 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 하거나 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 드라이버에서 SQL_SUCCESS_WITH_INFO를 반환할 때마다 드라이버 관리자에서 진단 정보를 가져옵니다 *hDbcInfoToken*, 응용 프로그램에 SQL_SUCCESS_WITH_INFO를 반환 하 고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)하 고 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
 응용 프로그램에서 사용 하는 경우 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)를 *wszOutConnectString* NULL 버퍼 (마지막 세 매개 변수는 모든 설정에 NULL, 0, NULL) 됩니다. 드라이버 응용 프로그램에 반환될지 출력 연결 문자열을 반환 해야이 고, 그렇지 [SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md) 호출 합니다.  
  
 ODBC 드라이버 개발을 위한 sqlspi.h 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
