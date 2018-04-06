---
title: SQLGetDiagRec 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 34aa67ed374f525f6195403b299500019192c19a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetDiagRec** 오류, 경고 및 상태 정보를 포함 하는 진단 레코드의 여러 필드의 현재 값을 반환 합니다. 와 달리 **SQLGetDiagField**, 호출별 진단 필드 하나를 반환 하는 **SQLGetDiagRec** 일반적으로 사용 되는 몇 가지 SQLSTATE, 원시 오류 코드를 포함 하 여 진단 레코드의 필드를 반환 하 고 진단 메시지 텍스트입니다.  
  
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
 [입력] 진단이 필요한 핸들의 형식을 설명 하는 핸들 형식 식별자입니다. 다음 중 하나여야 합니다.  
  
-   SQL_HANDLE_DBC 라는  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   여  
  
 드라이버 관리자와 드라이버는 경우에 SQL_HANDLE_DBC_INFO_TOKEN 핸들이 사용 됩니다. 응용 프로그램에는이 핸들 형식은 사용 하지 않아야 합니다. SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 참조 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.  
  
 *Handle*  
 [입력] 표시 된 형식의 진단 데이터 구조에 대 한 핸들 *HandleType*합니다. 경우 *HandleType* SQL_HANDLE_ENV은 *처리* 공유 또는 비공유 환경 핸들 일 수 있습니다.  
  
 *RecNumber*  
 [입력] 응용 프로그램 정보를 찾고 상태 레코드를 나타냅니다. 상태 레코드는 1에서 번호가 지정 됩니다.  
  
 *SQLState*  
 [출력] 진단 레코드에 대 한 5 자의 SQLSTATE 코드 (및 종료 NULL)를 반환 하는 버퍼에 대 한 포인터 *RecNumber*합니다. 처음 두 문자 클래스를 나타냅니다. 다음 세 하위 클래스를 나타냅니다. 이 정보는 SQL_DIAG_SQLSTATE 진단 필드에 포함 됩니다. 자세한 내용은 참조 [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)합니다.  
  
 *NativeErrorPtr*  
 [출력] 데이터 원본에 특정 원시 오류 코드를 반환 하는 버퍼에 대 한 포인터입니다. 이 정보는 SQL_DIAG_NATIVE 진단 필드에 포함 됩니다.  
  
 *MessageText*  
 [출력] 진단 메시지 텍스트 문자열을 반환 하는 버퍼에 대 한 포인터입니다. 이 정보는 SQL_DIAG_MESSAGE_TEXT 진단 필드에 포함 됩니다. 문자열의 형식에 대 한 참조 [진단 메시지](../../../odbc/reference/develop-app/diagnostic-messages.md)합니다.  
  
 경우 *MessageText* 이 NULL 이면 *TextLengthPtr* 문자 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 여전히 가리키는 버퍼에서 반환할 수 *MessageText*합니다.  
  
 *BufferLength*  
 [입력] 길이 **MessageText* 문자 단위의 버퍼입니다. 진단 메시지 텍스트의 최대 길이 없음 있습니다.  
  
 *TextLengthPtr*  
 [출력] 문자 (null 종결 문자에 대 한 필요한 문자 수는 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한  *\*MessageText*합니다. 반환할 수 있는 문자 개수 보다 큰 경우 *BufferLength*, 진단 메시지 텍스트에  *\*MessageText* 잘립니다 *BufferLength* null 종결 문자 길이 뺀 값입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDiagRec** 자체에 대 한 진단 레코드를 게시 하지 않습니다. 다음과 같은 반환 값의 자체 실행 결과 보고 하기 위해 사용 됩니다.  
  
-   SQL_SUCCESS: 함수가 진단 정보를 성공적으로 반환 했습니다.  
  
-   SQL_SUCCESS_WITH_INFO:는 \* *MessageText* 버퍼가 너무 작아서 요청한 진단 메시지를 저장할 수 있습니다. 진단 레코드가 생성 되었습니다. 잘림이 발생 한, 비교 해야 응용 프로그램을 확인 하려면 *BufferLength* 에 기록 되는 데 사용할 수 있는, 바이트의 실제 수 **StringLengthPtr*합니다.  
  
-   SQL_INVALID_HANDLE: 핸들이 표시 *HandleType* 및 *처리* 유효한 핸들 없습니다.  
  
-   SQL_ERROR 다음 중 하나가 발생 했습니다.:  
  
    -   *RecNumber* 음수 또는 0입니다.  
  
    -   *BufferLength* 가 0 보다 작습니다.  
  
    -   비동기 알림을 사용 하 여, 핸들에서 비동기 작업 완료 되지 않았습니다.  
  
-   SQL_NO_DATA: *RecNumber* 에 지정 된 핸들에 대 한 존재 하는 진단 레코드 개수 보다 큰 *처리 합니다.* 함수에 대 한 임의의 양수도 SQL_NO_DATA를 반환할 *RecNumber* 에 대 한 진단 레코드가 없는 경우 *처리*합니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 일반적으로 호출 **SQLGetDiagRec** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO ODBC 함수에 대 한 이전 호출에서 반환 하는 때입니다. 그러나 모든 ODBC 함수를 호출할 때마다 0 개 이상의 진단 레코드를 게시할 수 있습니다, 때문에 응용 프로그램이 호출할 수 **SQLGetDiagRec** ODBC 함수 호출 합니다. 응용 프로그램에서 호출할 수 **SQLGetDiagRec** 여러 번 진단 데이터 구조에서 일부 또는 모든 레코드를 반환 합니다. ODBC에서는 한 번에 저장할 수 있는 진단 레코드의 수를 제한 하지 않습니다.  
  
 **SQLGetDiagRec** 진단 데이터 구조의 헤더에서 필드를 반환할 사용할 수 없습니다. (의 *RecNumber* 인수는 0 보다 커야 합니다.) 응용 프로그램 호출 해야 **SQLGetDiagField** 이 목적을 위해 합니다.  
  
 **SQLGetDiagRec** 가장 최근에에 지정 된 핸들이와 관련 된 진단 정보를 검색 된 *처리* 인수입니다. 응용 프로그램이 다른 ODBC 함수를 호출 하는 경우를 제외 하 고 **SQLGetDiagRec**, **SQLGetDiagField**, 또는 **SQLError**에 대 한 이전 호출에서 모든 진단 정보는 동일한 핸들 손실 됩니다.  
  
 응용 프로그램에 검사할 수 모든 진단 레코드를 반복 하 여 증가 *RecNumber*로 **SQLGetDiagRec** 관계 없이 SQL_SUCCESS를 반환 합니다. 에 대 한 호출이 **SQLGetDiagRec** 는 헤더 및 레코드 필드에 비파괴적 합니다. 응용 프로그램에서 호출할 수 **SQLGetDiagRec** 으로 다른 함수를 제외 하 고 긴 처럼 레코드에서 필드를 검색 하려면 나중에 다시 **SQLGetDiagRec**, **SQLGetDiagField**, 또는 **SQLError**, 중간에 호출 되었습니다. 응용 프로그램 호출 하 여 사용할 수 있는 진단 레코드의 총 수를 검색할 수도 **SQLGetDiagField** 다음 호출 고 SQL_DIAG_NUMBER 필드의 값을 검색할 **SQLGetDiagRec**그 횟수입니다.  
  
 진단 데이터 구조의 필드에 대 한 참조 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다. 자세한 내용은 참조 [를 사용 하 여 SQLGetDiagRec 및 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 및 [SQLGetDiagRec 구현 및 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)합니다.  
  
 비동기적으로 실행 되는 것과 다른 API를 호출 하면 HY010 생성 됩니다 "함수 시퀀스 오류입니다."입니다. 그러나 비동기 작업이 완료 되기 전에 오류 레코드를 검색할 수 없습니다.  
  
## <a name="handletype-argument"></a>HandleType 인수  
 각 핸들 유형에 관련 된 진단 정보를 가질 수 있습니다. *HandleType* 인수 핸들 유형을 표시는 *처리* 인수입니다.  
  
 일부 헤더 및 레코드 필드는 핸들 환경, 연결, 문 및 설명자에 대 한 반환 수 없습니다. 필드 적용 되지 않는 이러한 핸들의 "헤더 필드" 및 "레코드 필드" 섹션에 표시 된 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)합니다.  
  
 에 대 한 호출 **SQLGetDiagRec** 경우 SQL_INVALID_HANDLE을 반환 합니다 *HandleType* 은 SQL_HANDLE_SENV는 공유 환경 핸들을 나타냅니다. 그러나 경우 *HandleType* SQL_HANDLE_ENV은 *처리* 공유 또는 비공유 환경 핸들 일 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|진단 레코드의 필드 또는 진단 헤더의 필드|[SQLGetDiagField 함수](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)
