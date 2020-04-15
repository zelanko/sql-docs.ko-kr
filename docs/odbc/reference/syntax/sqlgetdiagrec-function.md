---
title: SQLGetDiagRec 함수 | 마이크로 소프트 문서
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
ms.openlocfilehash: 39069526e254903509ddfef00b7bd4844f3d9e10
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285383"
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetDiagRec오류,** 경고 및 상태 정보를 포함하는 진단 레코드의 여러 필드의 현재 값을 반환합니다. 호출당 하나의 진단 필드를 반환하는 **SQLGetDiagField와**달리 **SQLGetDiagRec는** SQLSTATE, 기본 오류 코드 및 진단 메시지 텍스트를 포함하여 진단 레코드의 일반적으로 사용되는 여러 필드를 반환합니다.  
  
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
 [입력] 진단이 필요한 핸들 유형을 설명하는 핸들 형식 식별자입니다. 다음 중 하나여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 핸들은 드라이버 관리자와 드라이버에서만 사용됩니다. 응용 프로그램에서는 이 핸들 형식을 사용해서는 안 됩니다. SQL_HANDLE_DBC_INFO_TOKEN 대한 자세한 내용은 [ODBC 드라이버에서 연결-풀 인식 개발을](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)참조하십시오.  
  
 *Handle*  
 [입력] *핸들 Type으로*표시된 형식의 진단 데이터 구조에 대한 핸들입니다. *핸들유형이* SQL_HANDLE_ENV 경우 *핸들은* 공유 또는 공유되지 않은 환경 핸들일 수 있습니다.  
  
 *RecNumber*  
 [입력] 응용 프로그램에서 정보를 검색하는 상태 레코드를 나타냅니다. 상태 레코드는 1에서 번호가 매겨져 있습니다.  
  
 *Sqlstate*  
 [출력] 진단 레코드 *RecNumber에*대 한 5 자 SQLSTATE 코드 (및 NULL 종료)를 반환 하는 버퍼에 대 한 포인터 . 처음 두 문자는 클래스를 나타냅니다. 다음 세 개는 하위 클래스를 나타냅니다. 이 정보는 SQL_DIAG_SQLSTATE 진단 필드에 포함되어 있습니다. 자세한 내용은 [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)를 참조하십시오.  
  
 *네이티브 에이트에이펙트*  
 [출력] 데이터 원본에 특정한 기본 오류 코드를 반환할 버퍼에 대한 포인터입니다. 이 정보는 SQL_DIAG_NATIVE 진단 필드에 포함되어 있습니다.  
  
 *MessageText*  
 [출력] 진단 메시지 텍스트 문자열을 반환할 버퍼에 대한 포인터입니다. 이 정보는 SQL_DIAG_MESSAGE_TEXT 진단 필드에 포함되어 있습니다. 문자열의 형식은 진단 [메시지](../../../odbc/reference/develop-app/diagnostic-messages.md)를 참조하십시오.  
  
 *MessageText가* NULL인 경우 *TextLengthPtr은* *MessageText*로 가리키는 버퍼에서 반환할 수 있는 총 문자 수(문자 데이터에 대한 null 종료 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] 문자의 ** MessageText* 버퍼의 길이입니다. 진단 메시지 텍스트의 최대 길이가 없습니다.  
  
 *텍스트 길이Ptr*  
 [출력] * \*MessageText에서*반환할 수 있는 총 문자 수(null-termination 문자에 필요한 문자 수 제외)를 반환하는 버퍼에 대한 포인터입니다. 반환할 수 있는 문자 수가 *BufferLength보다*큰 경우 * \*MessageText의* 진단 메시지 텍스트는 Null 종료 문자의 길이를 뺀 *BufferLength로* 잘립니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetDiagRec** 자체에 대 한 진단 레코드를 게시 하지 않습니다. 다음 반환 값을 사용하여 자체 실행 결과를 보고합니다.  
  
-   SQL_SUCCESS: 함수가 진단 정보를 반환했습니다.  
  
-   SQL_SUCCESS_WITH_INFO: \* *MessageText* 버퍼가 너무 작아서 요청된 진단 메시지를 보류할 수 없습니다. 진단 레코드가 생성되지 않았습니다. 잘림이 발생했는지 확인하려면 응용 프로그램에서 *BufferLength를* **StringLengthPtr에*기록된 사용 가능한 실제 바이트 수와 비교해야 합니다.  
  
-   SQL_INVALID_HANDLE: HandleType *및* *Handle으로* 표시된 핸들이 올바른 핸들이 아닙니다.  
  
-   SQL_ERROR: 다음 중 하나가 발생했습니다.  
  
    -   *RecNumber는* 음수 또는 0입니다.  
  
    -   *버퍼길이가* 0보다 적습니다.  
  
    -   비동기 알림을 사용하는 경우 핸들의 비동기 작업이 완료되지 않았습니다.  
  
-   SQL_NO_DATA: *RecNumber핸들에* 지정된 핸들에 대해 존재했던 진단 레코드 수보다 *큽입니다.* 또한 이 함수는 *handle*에 대한 진단 레코드가 없는 경우 양수 *RecNumber에* 대해 SQL_NO_DATA 반환합니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램은 일반적으로 ODBC 함수에 대한 이전 호출이 SQL_ERROR 반환되거나 SQL_SUCCESS_WITH_INFO **경우 SQLGetDiagRec를** 호출합니다. 그러나 모든 ODBC 함수가 호출될 때마다 0 개 이상의 진단 레코드를 게시할 수 있으므로 응용 프로그램은 ODBC 함수 호출 후 **SQLGetDiagRec를** 호출할 수 있습니다. 응용 프로그램은 **SQLGetDiagRec를** 여러 번 호출하여 진단 데이터 구조의 일부 또는 전부를 반환할 수 있습니다. ODBC는 한 번에 저장할 수 있는 진단 레코드 수에 제한을 두지 않습니다.  
  
 **SQLGetDiagRec는** 진단 데이터 구조의 헤더에서 필드를 반환하는 데 사용할 수 없습니다. *(RecNumber* 인수는 0보다 커야 합니다.) 응용 프로그램은 이 목적을 위해 **SQLGetDiagField를** 호출해야 합니다.  
  
 **SQLGetDiagRec는** *핸들* 인수에 지정된 핸들과 가장 최근에 연결된 진단 정보만 검색합니다. 응용 프로그램이 **SQLGetDiagRec,** **SQLGetDiagField**또는 **SQLError를**제외한 다른 ODBC 함수를 호출하는 경우 동일한 핸들에서 이전 호출의 진단 정보가 손실됩니다.  
  
 응용 프로그램은 **SQLGetDiagRec가** SQL_SUCCESS 반환하는 한 *RecNumber를*증분하여 모든 진단 레코드를 검색할 수 있습니다. **SQLGetDiagRec에** 대한 호출은 헤더 및 레코드 필드에 비파괴적입니다. 응용 프로그램은 **SQLGetDiagRec** , **SQLGetDiagField**또는 **SQLError를**제외한 다른 함수가 없는 한 나중에 **SQLGetDiagRec를**다시 호출하여 레코드에서 필드를 검색할 수 있습니다. 또한 응용 프로그램은 **SQLGetDiagField를** 호출하여 SQL_DIAG_NUMBER 필드의 값을 검색한 다음 **SQLGetDiagRec를** 여러 번 호출하여 사용할 수 있는 총 진단 레코드 수를 검색할 수도 있습니다.  
  
 진단 데이터 구조의 필드에 대한 설명은 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)을 참조하십시오. 자세한 내용은 [SQLGetDiagRec 및 SQLGetDiagField 사용](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 및 [SQLGetDiagRec 및 SQLGetDiagField 구현을](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)참조하십시오.  
  
 비동기적으로 실행되는 API 이외의 API를 호출하면 HY010 "함수 시퀀스 오류"가 생성됩니다. 그러나 비동기 작업이 완료되기 전에는 오류 레코드를 검색할 수 없습니다.  
  
## <a name="handletype-argument"></a>핸들 타입 인수  
 각 핸들 유형에는 연결된 진단 정보가 있을 수 있습니다. *핸들 Type* 인수는 *핸들* 인수의 핸들 형식을 나타냅니다.  
  
 환경, 연결, 명령문 및 설명자 핸들에 대해 일부 헤더 및 레코드 필드를 반환할 수 없습니다. 필드가 적용되지 않는 핸들은 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)의 "헤더 필드" 및 "레코드 필드" 섹션에 표시됩니다.  
  
 *HANDLEType이* 공유 환경 핸들을 나타내는 SQL_HANDLE_SENV **경우 SQLGetDiagRec에** 대한 호출은 SQL_INVALID_HANDLE 반환합니다. 그러나 *handleType이* SQL_HANDLE_ENV 경우 *핸들은* 공유 또는 공유되지 않은 환경 핸들일 수 있습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|진단 레코드 필드 또는 진단 헤더 필드 구하기|[SQLGetDiagField 함수](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)
