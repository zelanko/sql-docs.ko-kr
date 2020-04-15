---
title: SQLConfigDriver 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0da15cef06e5d8392408108ce88b53f7885eb65e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301248"
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 함수
**규칙**  
 버전 소개: ODBC 2.5  
  
 **요약**  
 **SQLConfigDriver는** 적절한 드라이버 설정 DLL을 로드하고 **ConfigDriver** 함수를 호출합니다.  
  
 **SQLConfigDriver의** 기능은 ODBCCONF로 액세스할 수도 [있습니다. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
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
 *hwndParent*  
 [입력] 부모 창 핸들입니다. 핸들이 null이면 함수에 대화 상자가 표시되지 않습니다.  
  
 *f요청*  
 [입력] 요청 유형입니다. *fRequest는* 다음 값 중 하나를 포함해야 합니다.  
  
 ODBC_CONFIG_DRIVER: 드라이버에서 사용하는 연결 풀링 시간 단축을 변경합니다.  
  
 ODBC_INSTALL_DRIVER: 새 드라이버를 설치합니다.  
  
 ODBC_REMOVE_DRIVER: 기존 드라이버를 제거합니다.  
  
 이 옵션은 드라이버에 따라 다를 수 있으며, 이 경우 첫 번째 옵션에 대한 *fRequest는* ODBC_CONFIG_DRIVER_MAX+1부터 시작해야 합니다. 추가 옵션에 대한 *fRequest는* ODBC_CONFIG_DRIVER_MAX+1보다 큰 값에서 시작해야 합니다.  
  
 *lpsz드라이버*  
 [입력] 시스템 정보에 등록된 드라이버의 이름입니다.  
  
 *lpszArgs*  
 [입력] 드라이버 관련 *fRequest에*대한 인수를 포함하는 null-terminated 문자열입니다.  
  
 *lpszMsg*  
 [출력] 드라이버 설정에서 출력 메시지를 포함 하는 null-종료 된 문자열입니다.  
  
 *cbMsgMax*  
 [입력] *lpszMsg의 길이.*  
  
 *pcbMsgOut*  
 [출력] *lpszMsg로*반환할 수 있는 총 바이트 수입니다. 반환할 수 있는 바이트 수가 *cbMsgMax보다*크거나 같으면 *lpszMsg의* 출력 메시지는 null 종료 문자를 뺀 *cbmsgMax로* 잘립니다. *pcbMsgOut* 인수는 null 포인터일 수 있습니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLConfigDriver** FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 관련 된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못된 버퍼 길이|*lpszMsg* 인수가 잘못되었습니다.|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못되었습니다.|*hwndParent* 인수가 잘못되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못된 요청 유형|*fRequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> *fRequest* 인수는 ODBC_CONFIG_DRIVER_MAX 같지 않거나 같은 드라이버별 옵션입니다.|  
|ODBC_ERROR_INVALID_NAME|잘못된 드라이버 또는 번역기 이름|*lpszDriver* 인수가 잘못되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못된 키워드-값 쌍|*lpszArgs* 인수에는 구문 오류가 포함되어 있습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|설치 프로그램이 *fRequest* 인수에서 요청한 작업을 수행할 수 없습니다. **ConfigDriver에** 대한 호출이 실패했습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 번역기 설정 라이브러리를 로드할 수 없습니다.|드라이버 설정 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLConfigDriver는** 응용 프로그램이 이름을 알고 드라이버별 설정 DLL을 로드할 필요 없이 드라이버의 **ConfigDriver** 루틴을 호출할 수 있도록 합니다. 설치 프로그램은 드라이버 설치 DLL을 설치한 후 이 기능을 호출합니다. 호출 프로그램은 이 함수를 모든 드라이버에서 사용하지 못할 수 있음을 알고 있어야 합니다. 이 경우 호출 프로그램은 오류 없이 계속되어야 합니다.  
  
## <a name="driver-specific-options"></a>드라이버 별 옵션  
 응용 프로그램은 *fRequest* 인수를 사용하여 드라이버에서 노출되는 드라이버 관련 기능을 요청할 수 있습니다. 첫 번째 옵션에 대한 *fRequest는* ODBC_CONFIG_DRIVER_MAX+1이 되며 추가 옵션은 해당 값에서 1씩 증가합니다. 해당 함수에 대해 드라이버에 필요한 모든 인수는 *lpszArgs* 인수에 전달된 null-terminated 문자열에 제공되어야 합니다. 이러한 기능을 제공하는 드라이버는 드라이버 관련 옵션 테이블을 유지해야 합니다. 옵션은 드라이버 설명서에 완전히 문서화되어야 합니다. 드라이버 관련 옵션을 사용하는 응용 프로그램 작성기는 이 옵션을 사용하면 응용 프로그램의 상호 운용성이 낮아집니다.  
  
## <a name="setting-connection-pooling-timeout"></a>연결 풀링 시간 설정  
 드라이버 구성을 설정할 때 연결 풀링 시간 설정 속성을 설정할 수 있습니다. **SQLConfigDriver는** **cpTimeout으로**설정된 ODBC_CONFIG_DRIVER 및 *lpszArgs의* *fRequest로* 호출됩니다. **CPTimeout은** 연결을 사용하지 않고 연결 풀에 유지할 수 있는 기간을 결정합니다. 시간 시간이 만료되면 연결이 닫혀 풀에서 제거됩니다. 기본 시간 설정은 60초입니다.  
  
 **SQLConfigDriver가** ODBC_INSTALL_DRIVER 또는 ODBC_REMOVE_DRIVER *fRequest* 를 사용하여 호출되면 드라이버 관리자는 적절한 드라이버 설정 DLL을 로드하고 **ConfigDriver** 함수를 호출합니다. **SQLConfigDriverODBC_CONFIG_DRIVER** *의 fRequest를* 사용 하 고 있는 경우 모든 처리는 ODBC 설치 관리자에서 수행 되므로 드라이버 설치 DLL을 로드 할 필요가 없습니다.  
  
## <a name="messages"></a>메시지  
 드라이버 설치 루틴은 *lpszMsg* 버퍼에서 null 종료 문자열로 응용 프로그램에 문자 메시지를 보낼 수 있습니다. 메시지가 *cbMsgMax* 문자보다 크거나 같으면 **ConfigDriver** 함수에서 null 종료 문자를 뺀 *cmsgMax로* 잘립니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|드라이버 추가, 수정 또는 제거|[구성 드라이버(설정](../../../odbc/reference/syntax/configdriver-function.md)DLL)|  
|기본 데이터 원본 제거|[SQLRemoveDefault데이터 소스](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
