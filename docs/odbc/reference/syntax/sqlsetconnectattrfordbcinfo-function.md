---
title: SQLSetConnectAttrForDbcInfo 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f16cac6a715716dcef0a1c2b337716835c14b2b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67910369"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 함수
**규칙**  
 소개 된 버전: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLSetConnectAttrForDbcInfo** 는 **SQLSetConnectAttr**와 동일 하지만 연결 핸들 대신 연결 정보 토큰에 대 한 특성을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>인수  
 *hDbcInfoToken*  
 입력 토큰 핸들입니다.  
  
 *Attribute*  
 입력 설정할 특성입니다. 유효한 특성 목록은 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)에 대 한 드라이버와 동일 합니다.  
  
 *ValuePtr*  
 입력 *특성과*연결 될 값에 대 한 포인터입니다. *특성*의 값에 *따라, 이상 값은 32* 비트 부호 없는 정수 값이 되거나 null로 끝나는 문자열을 가리킵니다. *특성* 인수가 드라이버별 값인 경우에는 값이 Signed *eptr* 의 값이 부호 있는 정수일 수 있습니다.  
  
 *StringLength*  
 입력 *Attribute* 가 ODBC에 정의 된 *특성이 고 이상* 문자열이 문자열 또는 이진 버퍼를 가리키는 경우이 인수*는 *의 길이 여야 합니다.* 문자열 데이터의 경우이 인수는 문자열의 바이트 수를 포함 해야 합니다.  
  
 *Attribute* 가 ODBC에 정의 된 특성이 고 *valueptr* 이 정수 이면 *stringlength* 는 무시 됩니다.  
  
 *특성이* 드라이버 정의 특성인 경우 응용 프로그램은 *stringlength* 인수를 설정 하 여 특성의 특성을 드라이버 관리자에 게 표시 합니다. *Stringlength* 에는 다음 값을 사용할 수 있습니다.  
  
-   *Valueptr* 이 문자열에 대 한 포인터인 경우 *stringlength* 는 문자열 또는 SQL_NTS의 길이입니다.  
  
-   *Valueptr* 이 이진 버퍼에 대 한 포인터인 경우 응용 프로그램은 SQL_LEN_BINARY_ATTR (*length*) 매크로의 결과를 *stringlength*로 배치 합니다. 그러면 음수 값이 *Stringlength*에 배치 됩니다.  
  
-   *Valueptr* 이 문자열 또는 이진 문자열이 아닌 값에 대 한 포인터인 경우 *stringlength* 의 값은 SQL_IS_POINTER 이어야 합니다.  
  
-   *Valueptr* 이 고정 길이 값을 포함 하는 경우에는 *stringlength* 가 SQL_IS_INTEGER 또는 SQL_IS_UINTEGER입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)와 동일 합니다. 단, 드라이버 관리자는 **HandleType** 의 SQL_HANDLE_DBC_INFO_TOKEN 및 *Hdbcinfotoken*의 **핸들** 을 사용 합니다.  
  
## <a name="remarks"></a>설명  
 **SQLSetConnectAttrForDbcInfo** 는 **SQLSetConnectAttr**와 동일 하지만 연결 핸들 대신 연결 정보 토큰에 대 한 특성을 설정 합니다. 예를 들어 **SQLSetConnectAttr** 가 특성을 인식 하지 못하는 경우 **SQLSetConnectAttrForDbcInfo** 는 해당 특성에 대 한 SQL_ERROR도 반환 해야 합니다.  
  
 드라이버가 SQL_ERROR 또는 SQL_INVALID_HANDLE를 반환할 때마다 드라이버는이 특성을 무시 하 여 풀 ID를 계산 해야 합니다. 또한 드라이버 관리자는 *Hdbcinfotoken*에서 진단 정보를 가져오고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 및 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)의 응용 프로그램에 SQL_SUCCESS_WITH_INFO를 반환 합니다. 따라서 응용 프로그램에서 일부 특성을 설정할 수 없는 이유에 대 한 세부 정보를 검색할 수 있습니다.  
  
 응용 프로그램은이 함수를 직접 호출 하면 안 됩니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발용으로 sqlspi .h를 포함 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
