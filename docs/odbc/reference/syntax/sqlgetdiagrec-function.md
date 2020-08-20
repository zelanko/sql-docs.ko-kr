---
description: SQLGetDiagRec 함수
title: SQLGetDiagRec 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagRec
helpviewer_keywords:
- SQLGetDiagRec function [ODBC]
ms.assetid: ebdbac93-3d68-438f-8416-ef1f08e04269
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7f141891292fb80d53ba06e03329b66cbc8b826e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461016"
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 함수
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetDiagRec** 는 오류, 경고 및 상태 정보를 포함 하는 진단 레코드의 여러 필드에 대 한 현재 값을 반환 합니다. 호출 당 하나의 진단 필드를 반환 하는 **SQLGetDiagField**와 달리, **SQLGetDiagRec** 는 SQLSTATE, 네이티브 오류 코드 및 진단 메시지 텍스트를 포함 하 여 일반적으로 사용 되는 진단 레코드의 여러 필드를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetDiagRec(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLCHAR *       SQLState,  
     SQLINTEGER *    NativeErrorPtr,  
     SQLCHAR *       MessageText,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   TextLengthPtr);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 입력 진단이 필요한 핸들의 유형을 설명 하는 핸들 유형 식별자입니다. 다음 중 하나여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 핸들은 드라이버 관리자 및 드라이버 에서만 사용 됩니다. 응용 프로그램은이 핸들 형식을 사용 하면 안 됩니다. SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)을 참조 하세요.  
  
 *Handle*  
 입력 *HandleType*로 표시 되는 형식의 진단 데이터 구조에 대 한 핸들입니다. *HandleType* 가 SQL_HANDLE_ENV 경우 *handle* 은 공유 또는 공유 되지 않는 환경 핸들 일 수 있습니다.  
  
 *RecNumber*  
 입력 응용 프로그램에서 정보를 검색 하는 상태 레코드를 나타냅니다. 상태 레코드의 번호는 1입니다.  
  
 *SQLState*  
 출력 진단 레코드 *수*에 대 한 5 자로 된 SQLSTATE 코드를 반환 하 고 NULL을 종료 하는 버퍼에 대 한 포인터입니다. 처음 두 문자는 클래스를 의미 합니다. 다음 3 개는 하위 클래스를 의미 합니다. 이 정보는 SQL_DIAG_SQLSTATE 진단 필드에 포함 되어 있습니다. 자세한 내용은 [Sqlstates](../../../odbc/reference/develop-app/sqlstates.md)을 참조 하세요.  
  
 *NativeErrorPtr*  
 출력 네이티브 오류 코드를 반환할 버퍼에 대 한 포인터로, 데이터 소스에 해당 합니다. 이 정보는 SQL_DIAG_NATIVE 진단 필드에 포함 되어 있습니다.  
  
 *MessageText*  
 출력 진단 메시지 텍스트 문자열을 반환할 버퍼에 대 한 포인터입니다. 이 정보는 SQL_DIAG_MESSAGE_TEXT 진단 필드에 포함 되어 있습니다. 문자열의 형식은 [진단 메시지](../../../odbc/reference/develop-app/diagnostic-messages.md)를 참조 하세요.  
  
 *MessageText* 가 NULL 인 경우 *TextLengthPtr* 는 *MessageText*가 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 문자 데이터의 NULL 종료 문자를 제외한 총 문자 수를 반환 합니다.  
  
 *BufferLength*  
 입력 **MessageText* 버퍼의 길이 (문자)입니다. 진단 메시지 텍스트의 최대 길이는 없습니다.  
  
 *TextLengthPtr*  
 출력 * \* MessageText*에서 반환 하는 데 사용할 수 있는 총 문자 수 (null 종결 문자에 필요한 문자 수 제외)를 반환할 버퍼에 대 한 포인터입니다. 반환할 수 있는 문자 수가 *Bufferlength*보다 큰 경우 * \* MessageText* 의 진단 메시지 텍스트는 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDiagRec** 는 자체에 대 한 진단 레코드를 게시 하지 않습니다. 다음 반환 값을 사용 하 여 자체 실행의 결과를 보고 합니다.  
  
-   SQL_SUCCESS: 함수가 진단 정보를 성공적으로 반환 했습니다.  
  
-   SQL_SUCCESS_WITH_INFO: \* *MessageText* 버퍼가 너무 작아서 요청 된 진단 메시지를 저장할 수 없습니다. 진단 레코드를 생성 하지 않았습니다. 잘림이 발생 했는지 확인 하기 위해 응용 프로그램은 *Bufferlength* 를 사용 가능한 실제 바이트 수와 비교 하 여 **StringLengthPtr*에 기록 합니다.  
  
-   SQL_INVALID_HANDLE: *HandleType* 및 *handle* 이 나타내는 핸들이 유효한 핸들이 아닙니다.  
  
-   SQL_ERROR: 다음 중 하나가 발생 했습니다.  
  
    -   *값* 이 음수 이거나 0입니다.  
  
    -   *Bufferlength* 가 0 보다 작은 경우  
  
    -   비동기 알림을 사용 하는 경우 핸들에 대 한 비동기 작업이 완료 되지 않았습니다.  
  
-   SQL_NO_DATA: *값* 이 *핸들* 에 지정 된 핸들에 대해 존재 하는 진단 레코드 수보다 큽니다. 또한 함수는 *핸들*에 대 한 진단 레코드가 없는 경우 양수 *값* 에 대 한 SQL_NO_DATA를 반환 합니다.  
  
## <a name="comments"></a>주석  
 일반적으로 ODBC 함수에 대 한 이전 호출에서 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO을 반환 하면 응용 프로그램에서 **SQLGetDiagRec** 를 호출 합니다. 그러나 ODBC 함수는 호출 될 때마다 0 개 이상의 진단 레코드를 게시할 수 있으므로 응용 프로그램은 ODBC 함수 호출 후에 **SQLGetDiagRec** 를 호출할 수 있습니다. 응용 프로그램은 **SQLGetDiagRec** 를 여러 번 호출 하 여 진단 데이터 구조의 일부 또는 모든 레코드를 반환할 수 있습니다. ODBC에서는 한 번에 저장할 수 있는 진단 레코드 수에 제한이 없습니다.  
  
 **SQLGetDiagRec** 은 진단 데이터 구조의 헤더에서 필드를 반환 하는 데 사용할 수 없습니다. ( *값* 인수는 0 보다 커야 합니다.) 응용 프로그램은이 목적을 위해 **SQLGetDiagField** 를 호출 해야 합니다.  
  
 **SQLGetDiagRec** 는 *핸들* 인수에 지정 된 핸들과 가장 최근에 연결 된 진단 정보만 검색 합니다. 응용 프로그램에서 **SQLGetDiagRec**, **SQLGetDiagField**또는 **SQLError**를 제외 하 고 다른 ODBC 함수를 호출 하는 경우 동일한 핸들에 대 한 이전 호출의 진단 정보는 모두 손실 됩니다.  
  
 **SQLGetDiagRec** 가 *SQL_SUCCESS을 반환*하는 한 응용 프로그램은 모든 진단 레코드를 반복 해 서 검색할 수 있습니다. **SQLGetDiagRec** 에 대 한 호출은 헤더 및 레코드 필드에 대 한 비파괴입니다. 응용 프로그램은 나중에 **SQLGetDiagRec** 를 다시 호출 하 여 **SQLGetDiagRec**, **SQLGetDiagField**또는 **SQLError**를 제외한 다른 함수가 중간에서 호출 되지 않는 한 레코드에서 필드를 검색할 수 있습니다. 또한 응용 프로그램은 **SQLGetDiagField** 를 호출 하 여 SQL_DIAG_NUMBER 필드 값을 검색 한 다음 여러 번 **SQLGetDiagRec** 를 호출 하 여 사용할 수 있는 진단 레코드의 총 개수를 검색할 수 있습니다.  
  
 진단 데이터 구조의 필드에 대 한 설명은 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)를 참조 하세요. 자세한 내용은 [SQLGetDiagRec 및 SQLGetDiagField 사용](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 및 [SQLGetDiagRec 및 SQLGetDiagField 구현](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)을 참조 하세요.  
  
 비동기적으로 실행 되는 API 이외의 API를 호출 하면 "함수 시퀀스 오류" HY010 생성 됩니다. 그러나 비동기 작업이 완료 되기 전에는 오류 레코드를 검색할 수 없습니다.  
  
## <a name="handletype-argument"></a>HandleType 인수  
 각 핸들 유형에는 연결 된 진단 정보가 있을 수 있습니다. *HandleType* 인수는 *핸들* 인수의 핸들 형식을 나타냅니다.  
  
 환경, 연결, 문 및 설명자 핸들에 대해 일부 헤더 및 레코드 필드를 반환할 수 없습니다. 필드가 적용 되지 않는 핸들은 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)의 "헤더 필드" 및 "레코드 필드" 섹션에 나와 있습니다.  
  
 **SQLGetDiagRec** 호출은 공유 환경 핸들을 나타내는 *HandleType* 가 SQL_HANDLE_SENV 경우 SQL_INVALID_HANDLE를 반환 합니다. 그러나 *HandleType* 가 SQL_HANDLE_ENV 경우 *handle* 은 공유 또는 공유 되지 않는 환경 핸들 일 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|진단 레코드의 필드 또는 진단 헤더의 필드 가져오기|[SQLGetDiagField 함수](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)
