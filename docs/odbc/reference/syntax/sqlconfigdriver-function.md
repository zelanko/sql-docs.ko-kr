---
title: SQLConfigDriver 함수 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301248"
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 함수
**규칙**  
 소개 된 버전: ODBC 2.5  
  
 **요약**  
 **SQLConfigDriver** 는 적절 한 드라이버 설치 DLL을 로드 하 고 **configdriver** 함수를 호출 합니다.  
  
 ODBCCONF를 사용 하 여 **SQLConfigDriver** 의 기능에 액세스할 수도 있습니다 [. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 입력 부모 창 핸들입니다. 핸들이 null 이면 함수는 대화 상자를 표시 하지 않습니다.  
  
 *fRequest*  
 입력 요청 유형입니다. *Frequest* 는 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_CONFIG_DRIVER: 드라이버에서 사용 하는 연결 풀링 시간 제한을 변경 합니다.  
  
 ODBC_INSTALL_DRIVER: 새 드라이버를 설치 합니다.  
  
 ODBC_REMOVE_DRIVER: 기존 드라이버를 제거 합니다.  
  
 이 옵션은 드라이버에 국한 될 수도 있습니다 .이 경우 첫 번째 옵션에 대 한 *Frequest* 는 ODBC_CONFIG_DRIVER_MAX + 1부터 시작 해야 합니다. 또한 추가 옵션에 대 한 *Frequest* 는 ODBC_CONFIG_DRIVER_MAX + 1 보다 큰 값으로 시작 해야 합니다.  
  
 *lpszDriver*  
 입력 시스템 정보에 등록 된 드라이버의 이름입니다.  
  
 *lpszArgs*  
 입력 드라이버별 *Frequest*에 대 한 인수를 포함 하는 null로 끝나는 문자열입니다.  
  
 *lpszMsg*  
 출력 드라이버 설정의 출력 메시지를 포함 하는 null로 끝나는 문자열입니다.  
  
 *cbMsgMax*  
 입력 LpszMsg의 길이 *입니다.*  
  
 *pcbMsgOut*  
 출력 *LpszMsg*에서 반환할 수 있는 총 바이트 수입니다. 반환할 수 있는 바이트 수가 *Cbmsgmax*보다 크거나 같으면 *lpszMsg* 의 출력 메시지가 *cbmsgmax* 에서 null 종료 문자를 뺀 값으로 잘립니다. *Pcbmsgout* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLConfigDriver** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*LpszMsg* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못 되었습니다.|*HwndParent* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못 된 요청 유형|*Frequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> *Frequest* 인수는 ODBC_CONFIG_DRIVER_MAX 보다 작거나 같은 드라이버별 옵션입니다.|  
|ODBC_ERROR_INVALID_NAME|드라이버 또는 번역기 이름이 잘못 되었습니다.|*LpszDriver* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|*LpszArgs* 인수에 구문 오류가 포함 되어 있습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|설치 관리자가 *Frequest* 인수에서 요청 된 작업을 수행할 수 없습니다. **Configdriver** 를 호출 하지 못했습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 번역기 설치 라이브러리를 로드할 수 없습니다.|드라이버 설치 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLConfigDriver** 를 사용 하면 응용 프로그램에서 이름을 몰라도 드라이버의 **configdriver** 루틴을 호출할 수 있습니다. 드라이버 설치 DLL이 설치 된 후 설치 프로그램에서이 함수를 호출 합니다. 호출 프로그램은 모든 드라이버에 대해이 함수를 사용 하지 못할 수 있음을 알고 있어야 합니다. 이 경우 호출 프로그램은 오류 없이 계속 됩니다.  
  
## <a name="driver-specific-options"></a>드라이버 관련 옵션  
 응용 프로그램은 *Frequest* 인수를 사용 하 여 드라이버에서 제공 하는 드라이버 특정 기능을 요청할 수 있습니다. 첫 번째 옵션에 대 한 *Frequest* 는 ODBC_CONFIG_DRIVER_MAX + 1이 고 추가 옵션은 해당 값에서 1 씩 증가 합니다. 해당 함수에 대해 드라이버에 필요한 모든 인수는 *lpszArgs* 인수에 전달 된 null로 끝나는 문자열에 제공 해야 합니다. 이러한 기능을 제공 하는 드라이버는 드라이버별 옵션 테이블을 유지 해야 합니다. 이 옵션은 드라이버 설명서에 자세히 설명 되어 있습니다. 드라이버 관련 옵션을 사용 하는 응용 프로그램 작성자는 응용 프로그램의 상호 운용성을 줄여 주는 데이를 사용 한다는 점을 인식 해야 합니다.  
  
## <a name="setting-connection-pooling-timeout"></a>연결 풀링 제한 시간 설정  
 드라이버의 구성을 설정 하는 경우 연결 풀링 시간 제한 속성을 설정할 수 있습니다. **SQLConfigDriver** 는 ODBC_CONFIG_DRIVER의 *Frequest* 와 *lpszArgs* 를 **cptimeout**으로 설정 하 여 호출 됩니다. **Cptimeout** 은 연결이 사용 되지 않고 연결 풀에 남아 있을 수 있는 기간을 결정 합니다. 제한 시간이 만료 되 면 연결이 닫히고 풀에서 제거 됩니다. 기본 제한 시간은 60 초입니다.  
  
 *Frequest* 가 ODBC_INSTALL_DRIVER 또는 ODBC_REMOVE_DRIVER로 설정 된 상태에서 **SQLConfigDriver** 가 호출 되 면 드라이버 관리자는 적절 한 드라이버 설치 DLL을 로드 하 고 **configdriver** 함수를 호출 합니다. ODBC_CONFIG_DRIVER의 *Frequest* 를 사용 하 여 **SQLConfigDriver** 를 호출 하면 모든 처리가 ODBC 설치 관리자에서 수행 되므로 드라이버 설치 DLL을 로드할 필요가 없습니다.  
  
## <a name="messages"></a>메시지  
 드라이버 설치 루틴은 *lpszMsg* 버퍼에서 null로 종료 되는 문자열로 응용 프로그램에 문자 메시지를 보낼 수 있습니다. 이 메시지는 cbmsgmax가 *cbmsgmax* 문자 보다 크거나 같은 경우 **configdriver** 함수에서 null 종료 문자 *를 뺀 값* 으로 잘립니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|드라이버 추가, 수정 또는 제거|[Configdriver](../../../odbc/reference/syntax/configdriver-function.md)(설치 DLL)|  
|기본 데이터 소스 제거|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
