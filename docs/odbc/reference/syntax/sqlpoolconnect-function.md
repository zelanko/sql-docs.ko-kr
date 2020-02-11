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
ms.openlocfilehash: 0c390dacb5072c5d516e95b4fe6b789bfffbbd2d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68005806"
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect Function
**규칙**  
 소개 된 버전: ODBC 3.8 표준 준수: ODBC  
  
 **요약**  
 **Sqlpoolconnect** 는 풀의 연결을 다시 사용할 수 없는 경우 새 연결을 만드는 데 사용 됩니다.  
  
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
 입력 연결 핸들입니다.  
  
 *hDbcInfoToken*  
 입력 새 응용 프로그램 연결 요청에 대 한 토큰 핸들입니다.  
  
 *wszOutConnectString*  
 출력 완료 된 연결 문자열의 버퍼에 대 한 포인터입니다. 대상 데이터 원본에 성공적으로 연결 되 면이 버퍼에는 완료 된 연결 문자열이 포함 됩니다. 응용 프로그램은이 버퍼에 대해 최소 1024 문자를 할당 해야 합니다.  
  
 *WszOutConnectString* 가 NULL 인 경우 *Cchconnectstringlen* 은 *wszOutConnectString*가 가리키는 버퍼에서 반환 될 수 있는 총 문자 수 (문자 데이터의 NULL 종료 문자 제외)를 반환 합니다.  
  
 *cchConnectStringBuffer*  
 입력 **WszOutConnectString* 버퍼의 길이 (문자)입니다.  
  
 *cchConnectStringLen*  
 출력 \* *WszOutConnectString*에서 반환 하는 데 사용할 수 있는 총 문자 수 (null 종결 문자 제외)를 반환할 버퍼에 대 한 포인터입니다. 반환할 수 있는 문자 수가 *cchconnectstringbuffer*보다 크거나 같으면 \* *wszOutConnectString* 의 완료 된 연결 문자열이 *cchconnectstringbuffer* 에서 null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 입력 유효성 검사 오류에 대 한 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 와 유사 합니다. 단, 드라이버 관리자는 **HandleType** 의 SQL_HANDLE_DBC_INFO_TOKEN 및 *Hdbcinfotoken*의 **핸들** 을 사용 한다는 점을 제외 하면 됩니다.  
  
## <a name="remarks"></a>설명  
 드라이버 관리자는 *hDbc* 및 *Hdbcinfotoken* 의 부모 HENV 핸들이 동일 하도록 보장 합니다.  
  
 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)와 달리 사용자에 게 연결 정보를 입력 하 라는 메시지를 표시 하는 *drivercompletion* 인수가 없습니다. 메시지 표시 대화 상자는 풀링 시나리오에서 허용 되지 않습니다.  
  
 응용 프로그램은이 함수를 직접 호출 하면 안 됩니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 드라이버가 SQL_ERROR 또는 SQL_INVALID_HANDLE를 반환할 때마다 드라이버 관리자는 오류를 응용 프로그램 ( [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 또는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))으로 반환 합니다.  
  
 드라이버가 SQL_SUCCESS_WITH_INFO를 반환할 때마다 드라이버 관리자는 *Hdbcinfotoken*에서 진단 정보를 가져오고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 및 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)의 응용 프로그램에 SQL_SUCCESS_WITH_INFO을 반환 합니다.  
  
 응용 프로그램에서 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)를 사용 하는 경우 *wszOutConnectString* 는 null 버퍼가 됩니다. 마지막 세 매개 변수는 모두 NULL, 0, null로 설정 됩니다. 그렇지 않으면 드라이버가 응용 프로그램의 [SQLDriverConnect 함수](../../../odbc/reference/syntax/sqldriverconnect-function.md) 호출로 반환 되는 출력 연결 문자열을 반환 해야 합니다.  
  
 ODBC 드라이버 개발용으로 sqlspi .h를 포함 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
