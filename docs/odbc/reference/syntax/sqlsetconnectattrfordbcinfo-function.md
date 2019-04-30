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
manager: craigg
ms.openlocfilehash: 798f986adfeda95ef091161458d94c2ccc33b2e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63125536"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 함수
**규칙**  
 도입 된 버전: ODBC 3.81 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLSetConnectAttrForDbcInfo** 같습니다 **SQLSetConnectAttr**, 하지만 연결 핸들에 연결 정보 토큰 대신에 특성을 설정 하는 것입니다.  
  
## <a name="syntax"></a>구문  
  
```  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>인수  
 *hDbcInfoToken*  
 [입력] 토큰 핸들입니다.  
  
 *특성*  
 [입력] 설정할 특성입니다. 유효한 특성 목록에는 특정 드라이버 및과 동일 하 게 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)합니다.  
  
 *ValuePtr*  
 [입력] 와 연결할 값에 대 한 포인터 *특성*합니다. 값에 따라 *특성*하십시오 *ValuePtr* 32 비트 부호 없는 정수 값 또는 null로 끝나는 문자열을 가리킵니다. 경우는 *특성* 인수는 드라이버별 값, 값 *ValuePtr* 부호 있는 정수를 수 있습니다.  
  
 *StringLength*  
 [입력] 하는 경우 *특성* 은 ODBC 정의 특성 및 *ValuePtr* 문자열 또는 이진 버퍼를 가리키는,이 인수 길이 여야 합니다 **ValuePtr*합니다. 문자 문자열 데이터의 경우이 인수는 문자열의 바이트 수를 포함 해야 합니다.  
  
 하는 경우 *특성* 은 ODBC 정의 특성 및 *ValuePtr* 정수 이면 *StringLength* 무시 됩니다.  
  
 하는 경우 *특성* 은 드라이버에서 정의 된 특성을 응용 프로그램을 설정 하 여 드라이버 관리자에 특성의 특성을 나타내는 합니다 *StringLength* 인수. *StringLength* 다음 값을 가질 수 있습니다.  
  
-   하는 경우 *ValuePtr* 문자열에 대 한 포인터 이면 *StringLength* SQL_NTS 또는 문자열의 길이입니다.  
  
-   하는 경우 *ValuePtr* 이진 버퍼에 대 한 포인터 이면 응용 프로그램을 SQL_LEN_BINARY_ATTR의 결과 배치 (*길이*)에서 매크로 *StringLength*합니다. 에 음수 값이 배치 *StringLength*합니다.  
  
-   하는 경우 *ValuePtr* 이 아닌 문자열 또는 이진 문자열 값에 대 한 포인터 이면 *StringLength* SQL_IS_POINTER 값이 있어야 합니다.  
  
-   하는 경우 *ValuePtr* 다음을 고정 길이 값이 포함 되어 *StringLength* SQL_IS_INTEGER 또는 SQL_IS_UINTEGER를 적절 하 게 됩니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 동일 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)드라이버 관리자를 사용 한다는 점을 제외 하면는 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN의와 **처리할** 의 *hDbcInfoToken* .  
  
## <a name="remarks"></a>Remarks  
 **SQLSetConnectAttrForDbcInfo** 같습니다 **SQLSetConnectAttr**, 하지만 연결 핸들에 연결 정보 토큰에 대 한 특성 대신 설정 합니다. 예를 들어 경우 **SQLSetConnectAttr** 특성을 인식 하지 못하는 **SQLSetConnectAttrForDbcInfo** 해당 특성에 대 한도 SQL_ERROR를 반환 해야 합니다.  
  
 드라이버 풀 ID를 계산 하려면이 특성을 무시 해야 드라이버가 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환 될 때마다 또한 드라이버 관리자에서 진단 정보를 가져옵니다 *hDbcInfoToken*, 응용 프로그램에 SQL_SUCCESS_WITH_INFO를 반환 하 고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 고 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). 따라서 응용 프로그램 몇 가지 특성을 설정할 수 없습니다는 이유는 무엇에 대 한 정보를 검색할 수 있습니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발을 위한 sqlspi.h 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
