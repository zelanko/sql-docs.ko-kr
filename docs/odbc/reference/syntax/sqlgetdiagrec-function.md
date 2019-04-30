---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab81694fb0234a896a7e9fd09d338e8db43360eb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259332"
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLGetDiagRec** 오류, 경고 및 상태 정보가 포함 된 진단 레코드의 여러 필드의 현재 값을 반환 합니다. 와 달리 **SQLGetDiagField**, 호출 당 하나의 진단 필드를 반환 하는 **SQLGetDiagRec** 일반적으로 사용 되는 여러 SQLSTATE, 원시 오류 코드를 포함 하 여 진단 레코드의 필드를 반환 하 고 진단 메시지 텍스트입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 진단이 필요 하는 핸들의 형식을 설명 하는 핸들 형식 식별자입니다. 다음 중 하나여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 드라이버 관리자 및 드라이버에 의해서만 SQL_HANDLE_DBC_INFO_TOKEN 핸들을 사용 합니다. 응용 프로그램에는이 핸들 형식은 사용 하지 마십시오. SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 참조 하세요. [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.  
  
 *Handle*  
 [입력] 지정 된 형식의 진단 데이터 구조에 대 한 핸들 *HandleType*합니다. 하는 경우 *HandleType* SQL_HANDLE_ENV, 됩니다 *처리* 공유 또는 비공유 환경 핸들 일 수 있습니다.  
  
 *RecNumber*  
 [입력] 응용 프로그램 정보를 검색 하는 상태 레코드를 나타냅니다. 상태 레코드는 1부터 번호가 지정 됩니다.  
  
 *SQLState*  
 [출력] 진단 레코드에 대 한 5 자의 SQLSTATE 코드 (및 종결 NULL)를 반환 하는 버퍼에 대 한 포인터 *RecNumber*합니다. 처음 두 문자를 나타내는 클래스입니다. 다음 세 하위 클래스를 나타냅니다. 이 정보는 SQL_DIAG_SQLSTATE 진단 필드에 포함 됩니다. 자세한 내용은 [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)합니다.  
  
 *NativeErrorPtr*  
 [출력] 특정 데이터 원본에는 원시 오류 코드를 반환 하는 버퍼에 대 한 포인터입니다. 이 정보는 SQL_DIAG_NATIVE 진단 필드에 포함 됩니다.  
  
 *MessageText*  
 [출력] 진단 메시지 텍스트 문자열을 반환 하는 버퍼에 대 한 포인터입니다. 이 정보는 SQL_DIAG_MESSAGE_TEXT 진단 필드에 포함 됩니다. 문자열의 형식에 대해서 [진단 메시지](../../../odbc/reference/develop-app/diagnostic-messages.md)합니다.  
  
 경우 *MessageText* 가 null 인 경우 *TextLengthPtr* (문자 데이터에 대 한 null 종료 문자를 제외한) 문자의 총 수를 반환 여전히가 가리키는 버퍼에서 반환할 사용 가능한 *MessageText*합니다.  
  
 *BufferLength*  
 [입력] 길이 **MessageText* 문자에서 버퍼입니다. 진단 메시지 텍스트의 최대 길이가 없습니다.  
  
 *TextLengthPtr*  
 [출력] 문자 (null 종료 문자에 필요한 문자 수 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한  *\*MessageText*합니다. 반환할 사용 가능한 문자 개수 보다 크면 *BufferLength*에서 진단 메시지 텍스트  *\*MessageText* 잘립니다 *BufferLength* null 종료 문자 길이 뺀 값입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDiagRec** 자체에 대 한 진단 레코드를 게시 하지 않습니다. 자체 실행의 결과 보고 하는 다음 반환 값을 사용 합니다.  
  
-   SQL_SUCCESS: 함수는 진단 정보를 반환 했습니다.  
  
-   SQL_SUCCESS_WITH_INFO: 합니다 \* *MessageText* 버퍼가 너무 작아서 요청 된 진단 메시지를 저장할 수 있습니다. 진단 레코드가 생성 되었습니다. 잘림이 발생을 응용 프로그램을 비교 해야 결정할 *BufferLength* 에 기록 되는 사용 가능한 바이트의 실제 수 **StringLengthPtr*합니다.  
  
-   SQL_INVALID_HANDLE: 핸들에 나타난 *HandleType* 하 고 *처리* 는 유효한 핸들이 없습니다.  
  
-   SQL_ERROR: 다음 중 하나에 다음이 발생 했습니다.  
  
    -   *RecNumber* 가 음수 이거나 0입니다.  
  
    -   *BufferLength* 가 0 보다 작습니다.  
  
    -   비동기 알림을 사용 하는 경우 핸들에 대해 비동기 작업이 완료 되지 않았습니다.  
  
-   SQL_NO_DATA: *RecNumber* 에 지정 된 핸들에 대해 존재 하는 진단 레코드 개수 보다 *처리 합니다.* 또한 함수 모든 양수 SQL_NO_DATA를 반환할 *RecNumber* 에 대 한 진단 레코드가 없는 경우 *처리*합니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 일반적으로 호출 **SQLGetDiagRec** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO ODBC 함수에 대 한 이전 호출에 반환 하는 경우. 그러나 모든 ODBC 함수를 호출할 때마다 0 개 이상의 진단 레코드를 게시할 수, 때문에 응용 프로그램이 호출할 수 있습니다 **SQLGetDiagRec** ODBC 함수를 호출 합니다. 응용 프로그램에서 호출할 수 있습니다 **SQLGetDiagRec** 여러 번 진단 데이터 구조에서 일부 또는 모든 레코드를 반환 합니다. ODBC에서는 한 번에 저장할 수 있는 진단 레코드의 수를 제한 하지 않습니다.  
  
 **SQLGetDiagRec** 진단 데이터 구조의 헤더에서 필드를 반환 하려면 사용할 수 없습니다. (합니다 *RecNumber* 인수는 0 보다 커야 합니다.) 응용 프로그램을 호출 해야 **SQLGetDiagField** 이 목적입니다.  
  
 **SQLGetDiagRec** 에 지정 된 핸들을 사용 하 여 가장 최근에 연결 된 진단 정보를 검색 합니다 *처리* 인수입니다. 다른 ODBC 함수를 호출 하는 응용 프로그램을 제외한 **SQLGetDiagRec**를 **SQLGetDiagField**, 또는 **SQLError**에 대 한 이전 호출에서 모든 진단 정보는 동일한 핸들 손실 됩니다.  
  
 응용 프로그램 수 검색 모든 진단 레코드를 반복 하 여 증분 *RecNumber*으로 **SQLGetDiagRec** 관계 없이 SQL_SUCCESS를 반환 합니다. 에 대 한 호출 **SQLGetDiagRec** 헤더 및 레코드 필드에 비 소멸 됩니다. 응용 프로그램에서 호출할 수 있습니다 **SQLGetDiagRec** 이상으로 다른 함수를 제외 하 고 오래 된 레코드에서 필드를 검색 하려면 나중에 다시 **SQLGetDiagRec**하십시오 **SQLGetDiagField**, 또는 **SQLError**를 중간에서 호출 했습니다. 응용 프로그램 호출 하 여 사용할 수 있는 진단 레코드의 총 수를 검색할 수도 **SQLGetDiagField** SQL_DIAG_NUMBER 필드 및 호출의 값을 검색할 **SQLGetDiagRec**횟수입니다.  
  
 진단 데이터 구조의 필드에 대 한 참조 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다. 자세한 내용은 [를 사용 하 여 SQLGetDiagRec 및 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 하 고 [구현 SQLGetDiagRec 및 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)합니다.  
  
 비동기적으로 실행 되는 것과 다른 API를 호출할 HY010 생성 "함수 시퀀스 오류입니다."입니다. 그러나 비동기 작업이 완료 되기 전에 오류 레코드를 검색할 수 없습니다.  
  
## <a name="handletype-argument"></a>HandleType 인수  
 각 핸들 형식은 연결 된 진단 정보를 가질 수 있습니다. *HandleType* 인수 핸들 유형을 표시 합니다 *처리* 인수입니다.  
  
 일부 헤더 및 레코드 필드는 핸들 환경, 연결, 문 및 설명자에 대 한 반환 수 없습니다. "헤더 필드" 및 "레코드 필드" 섹션에는 필드를 적용할 수 없는 이러한 핸들이 표시 됩니다 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다.  
  
 에 대 한 호출 **SQLGetDiagRec** 하면 SQL_INVALID_HANDLE 반환 됩니다 *HandleType* 는 SQL_HANDLE_SENV 공유 환경 핸들을 나타냅니다. 그러나 경우 *HandleType* SQL_HANDLE_ENV, 됩니다 *처리* 공유 또는 비공유 환경 핸들 일 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|진단 레코드의 필드 또는 진단 헤더 필드 가져오기|[SQLGetDiagField 함수](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)
