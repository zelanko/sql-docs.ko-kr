---
title: SQLPoolConnect 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 141ba45aca6a6bcc25503ef73d575793f1cf5b15
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect 함수
**규칙**  
 도입 된 버전: ODBC 3.8 표준 준수: ODBC  
  
 **요약**  
 **SQLPoolConnect** 연결 풀에서 다시 사용할 수 있으면 새 연결을 만드는 데 사용 됩니다.  
  
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
 [입력] 새 응용 프로그램 연결 요청에 대 한 토큰 핸들입니다.  
  
 *wszOutConnectString*  
 [출력] 완료 된 연결 문자열에 대 한 버퍼에 대 한 포인터입니다. 대상 데이터 원본에 연결 성공 시이 버퍼는 완료 된 연결 문자열을 포함합니다. 이 버퍼에 대 한 응용 프로그램 적어도 1, 024 자로 할당 해야 합니다.  
  
 경우 *wszOutConnectString* 이 NULL 이면 *cchConnectStringLen* 여전히 문자 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 합니다에 반환할 사용할 수는 버퍼에서 가리키는 *wszOutConnectString*합니다.  
  
 *cchConnectStringBuffer*  
 [입력] 길이 **wszOutConnectString* 문자에서 버퍼입니다.  
  
 *cchConnectStringLen*  
 [출력] 문자 (null 종결 문자 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *wszOutConnectString*합니다. 반환할 수 있는 문자 수는 보다 크거나 같은 경우 *cchConnectStringBuffer*, 연결 문자열에서 완료 \* *wszOutConnectString* 잘립니다*cchConnectStringBuffer* null 종결 문자 길이 뺀 값입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 비슷합니다 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 제외 드라이버 관리자에서 사용 하 고 유효성 검사 오류를 입력 한 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN의 및 **처리** 의 *hDbcInfoToken*합니다.  
  
## <a name="remarks"></a>주의  
 드라이버 관리자의 처리 HENV 부모 보장 *hDbc* 및 *hDbcInfoToken* 동일 합니다.  
  
 와 달리 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)는 없는 *DriverCompletion* 인수를 사용자가 연결 정보를 입력 하도록 메시지를 표시 합니다. 묻는 대화 상자가 풀링 시나리오에서 허용 되지 않습니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지원 되는 ODBC 드라이버가이 함수를 구현 해야 합니다.  
  
 드라이버 관리자 응용 프로그램에 오류를 반환 하는 드라이버 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환 될 때마다 (에서 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 또는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 드라이버 관리자의 진단 정보를 가져옵니다는 드라이버에서 SQL_SUCCESS_WITH_INFO를 반환할 때마다 *hDbcInfoToken*, 응용 프로그램에 sql_success_with_info가 반환 하 고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)및 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
 응용 프로그램 사용 하는 경우 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), *wszOutConnectString* NULL 버퍼 (마지막 세 매개 변수는 모든 설정에 NULL, 0, NULL) 됩니다. 드라이버 돌아갑니다 응용 프로그램의 출력 연결 문자열을 반환 해야 그렇지 않으면 [SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md) 호출 합니다.  
  
 ODBC 드라이버 개발에 대 한 sqlspi.h를 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 드라이버를 개발합니다.](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
