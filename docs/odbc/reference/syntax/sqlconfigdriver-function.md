---
title: SQLConfigDriver 함수 | Microsoft Docs
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
- SQLConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDriver
helpviewer_keywords:
- SQLConfigDriver function [ODBC]
ms.assetid: 4f681961-ac9f-4d88-b065-5258ba112642
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3af2f70156cae3427b5d22f3214f5c911af14a5d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 함수
**규칙**  
 2.5 ODBC에 도입 된 버전:  
  
 **요약**  
 **SQLConfigDriver** 적절 한 드라이버 설치 DLL 및 호출 로드는 **ConfigDriver** 함수입니다.  
  
 기능 **SQLConfigDriver** 로 액세스할 수도 [ODBCCONF 합니다. EXE](../../../odbc/odbcconf-exe.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLConfigDriver(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszArgs,  
     LPSTR    lpszMsg,  
     WORD     cbMsgMax,  
     WORD *   pcbMsgOut);  
```  
  
## <a name="arguments"></a>인수  
 *창은*  
 [입력] 부모 창 핸들입니다. 핸들 null 이면 함수는 모든 대화 상자 표시 되지 않습니다.  
  
 *문제점과*  
 [입력] 요청의 유형입니다. *문제점과* 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_CONFIG_DRIVER: 연결 풀링 드라이버에서 사용 하는 제한 시간을 변경 합니다.  
  
 ODBC_INSTALL_DRIVER: 새 드라이버를 설치합니다.  
  
 ODBC_REMOVE_DRIVER: 기존 드라이버를 제거합니다.  
  
 이 옵션 또한 수 드라이버 관련은 쿼리에서 *문제점과* 첫 번째 옵션 ODBC_CONFIG_DRIVER_MAX + 1에서 시작 해야 합니다. *문제점과* 에 추가 옵션 ODBC_CONFIG_DRIVER_MAX + 1 보다 큰 값에서 시작 해야 합니다.  
  
 *lpszDriver*  
 [입력] 시스템 정보에 등록 된 드라이버의 이름입니다.  
  
 *lpszArgs*  
 [입력] 드라이버 관련에 대 한 인수를 포함 하는 null로 끝나는 문자열 *문제점과*합니다.  
  
 *lpszMsg*  
 [출력] Null로 끝나는 문자열 드라이버 설치 프로그램에서 출력 메시지를 포함 하는 데 사용 합니다.  
  
 *cbMsgMax*  
 [입력] 길이 *lpszMsg 합니다.*  
  
 *pcbMsgOut*  
 [출력] 반환 하려면 사용 가능한 바이트의 총 수 *lpszMsg*합니다. 보다 크거나 반환에 사용할 수 있는 바이트 수가 *cbMsgMax*, 출력 메시지에 *lpszMsg* 잘립니다 *cbMsgMax* 뺀 null 종료 문자입니다. *pcbMsgOut* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLConfigDriver** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*lpszMsg* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_HWND|잘못 된 창 핸들|*창은* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|*문제점과* 인수는 다음 중 하나 였습니다.<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> *문제점과* ODBC_CONFIG_DRIVER_MAX 보다 작은 드라이버 관련 옵션에 인수가 있습니다.|  
|ODBC_ERROR_INVALID_NAME|잘못 된 드라이버 또는 변환기 이름입니다.|*lpszDriver* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|*lpszArgs* 인수에 구문 오류가 포함 되어 있습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|설치 관리자가 요청한 작업을 수행할 수 없습니다는 *문제점과* 인수입니다. 에 대 한 호출 **ConfigDriver** 실패 했습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 변환기 설치 라이브러리를 로드할 수 없습니다.|드라이버 설치 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 **SQLConfigDriver** 운전 호출 응용 프로그램 **ConfigDriver** 이름을 알고와 드라이버 설치 DLL을 로드할 필요 없이 라우팅입니다. 설치 프로그램 드라이버 설치 DLL을 설치한 후이 함수를 호출 합니다. 호출 프로그램은이 함수 사용 하지 못할 모든 드라이버에 대해 알고 있어야 합니다. 이 경우 호출 프로그램은 오류 없이 계속 해야 합니다.  
  
## <a name="driver-specific-options"></a>드라이버 관련 옵션  
 응용 프로그램 사용 하 여 드라이버에 의해 노출 되는 드라이버 관련 기능을 요청할 수는 *문제점과* 인수입니다. *문제점과* 첫 번째 옵션은 ODBC_CONFIG_DRIVER_MAX + 1, 수 및 추가 옵션을 해당 값에서 1 씩 증가 합니다. 전달 된 null로 끝나는 문자열에 제공 해야 해당 함수에 대 한 드라이버에 필요한 모든 인수는 *lpszArgs* 인수입니다. 이러한 기능을 제공 하는 드라이버는 드라이버 관련 옵션의 테이블을 유지 해야 합니다. 옵션은 드라이버 설명서의 완전히 문서화 해야 합니다. 드라이버 관련 옵션을 사용 하는 응용 프로그램 작성자는이 처럼 사용 하면 응용 프로그램 덜 상호 운용 가능한 알고 있어야 합니다.  
  
## <a name="setting-connection-pooling-timeout"></a>연결 풀링 시간 제한 설정  
 드라이버의 구성을 설정 하는 경우에 연결 풀링 시간 제한 속성을 설정할 수 있습니다. **SQLConfigDriver** 로 호출 되는 *문제점과* ODBC_CONFIG_DRIVER의 및 *lpszArgs* 로 설정 **CPTimeout**합니다. **CPTimeout** 연결을 사용 하지 않고 연결 풀에서 유지 될 수 있는 기간을 결정 합니다. 제한 시간이 만료 되 면 연결이 닫히고 풀에서 제거 합니다. 기본 제한 시간은 60 초입니다.  
  
 때 **SQLConfigDriver** 사용 하 여 호출 *문제점과* ODBC_INSTALL_DRIVER 또는 ODBC_REMOVE_DRIVER로 설정, 드라이버 관리자 로드 적절 한 드라이버 설치 DLL 및 호출 된  **ConfigDriver** 함수입니다. 때 **SQLConfigDriver** 로 호출 되는 *문제점과* ODBC_CONFIG_DRIVER의 모든 처리가 수행 되는 ODBC 설치 관리자에 드라이버 설치 DLL에서 로드 되지 않도록 합니다.  
  
## <a name="messages"></a>메시지  
 드라이버 설치 루틴에서 null로 끝나는 문자열로 응용 프로그램에 문자 메시지를 보낼 수는 *lpszMsg* 버퍼입니다. 메시지가 잘릴 수 *cbMsgMax* 뺀 하 여 null 종결 문자는 **ConfigDriver** 보다 크거나 같은 경우에 작동 *cbMsgMax* 문자입니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 드라이버를 제거 합니다.|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(에 DLL 설치)|  
|기본 데이터 원본 제거|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
