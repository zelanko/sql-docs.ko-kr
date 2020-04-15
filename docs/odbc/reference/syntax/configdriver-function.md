---
title: 구성 드라이버 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDriver
helpviewer_keywords:
- ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a2da5fd5ce01bd97f13d7c8d805c615c1ac436a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303964"
---
# <a name="configdriver-function"></a>ConfigDriver 함수
**규칙**  
 버전 소개: ODBC 2.5  
  
 **요약**  
 **ConfigDriver는** 설치 프로그램이 **ConfigDSN을**호출할 필요 없이 설치 및 제거 기능을 수행할 수 있도록 합니다. 이 기능은 설치 중 드라이버 별 시스템 정보 생성 및 DSN 변환 수행, 제거 시 시스템 정보 수정 정리와 같은 드라이버 별 기능을 수행합니다. 이 기능은 드라이버 설정 DLL 또는 별도의 설치 DLL에 의해 노출됩니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL ConfigDriver(  
      HWND    hwndParent,  
      WORD    fRequest,  
      LPCSTR  lpszDriver,  
      LPCSTR  lpszArgs,  
      LPSTR   lpszMsg,  
      WORD    cbMsgMax,  
      WORD *  pcbMsgOut);  
```  
  
## <a name="arguments"></a>인수  
 *hwndParent*  
 [입력] 부모 창 핸들입니다. 핸들이 null이면 함수에 대화 상자가 표시되지 않습니다.  
  
 *f요청*  
 [입력] 요청 유형입니다. *fRequest* 인수에는 다음 값 중 하나가 포함되어야 합니다.  
  
 ODBC_INSTALL_DRIVER: 새 드라이버를 설치합니다.  
  
 ODBC_REMOVE_DRIVER: 드라이버를 제거합니다.  
  
 이 옵션은 드라이버에 따라 다를 수 있으며, 이 경우 첫 번째 옵션에 대한 *fRequest* 인수는 ODBC_CONFIG_DRIVER_MAX+1부터 시작해야 합니다. 추가 옵션에 대한 *fRequest* 인수도 ODBC_CONFIG_DRIVER_MAX+1보다 큰 값에서 시작해야 합니다.  
  
 *lpsz드라이버*  
 [입력] 시스템 정보의 Odbcinst.ini 키에 등록된 드라이버의 이름입니다.  
  
 *lpszArgs*  
 [입력] 드라이버 관련 *fRequest에*대한 인수를 포함하는 null-terminated 문자열 .  
  
 *lpszMsg*  
 [출력] 드라이버 설정에서 출력 메시지를 포함 하는 null-종료 된 문자열입니다.  
  
 *cbMsgMax*  
 [입력] *lpszMsg의*길이 .  
  
 *pcbMsgOut*  
 [출력] *lpszMsg로*반환할 수 있는 총 바이트 수입니다.  
  
 반환할 수 있는 바이트 수가 *cbMsgMax보다*크거나 같으면 *lpszMsg의* 출력 메시지는 null 종료 문자를 뺀 *cbmsgMax로* 잘립니다. *pcbMsgOut* 인수는 null 포인터일 수 있습니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **ConfigDriver** FALSE를 반환 하는 경우 관련 된 * \*pfErrorCode* 값 **SQLPostInstallerError에** 대 한 호출에 의해 설치 관리자 오류 버퍼에 게시 되 고 **SQLInstallerError**를 호출 하 여 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못되었습니다.|*hwndParent* 인수가 잘못되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못된 요청 유형|*fRequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> 드라이버 별 옵션은 ODBC_CONFIG_DRIVER_MAX 같지 않거나 동일했습니다.|  
|ODBC_ERROR_INVALID_NAME|잘못된 드라이버 또는 번역기 이름|*lpszDriver* 인수가 잘못되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|*fRequest* 인수에서 요청한 작업을 수행할 수 없습니다.|  
|ODBC_ERROR_DRIVER_SPECIFIC|드라이버 또는 번역기 관련 오류|정의된 ODBC 설치 관리자 오류가 없는 드라이버별 오류입니다. **SQLPostInstallerError** 함수에 대 한 호출에서 *SzError* 인수 드라이버 관련 오류 메시지를 포함 해야 합니다.|  
  
## <a name="comments"></a>주석  
  
### <a name="driver-specific-options"></a>드라이버 별 옵션  
 응용 프로그램은 *fRequest* 인수를 사용하여 드라이버에서 노출되는 드라이버 관련 기능을 요청할 수 있습니다. 첫 번째 옵션에 대한 *fRequest는* ODBC_CONFIG_DRIVER_MAX 1이 되고 추가 옵션은 해당 값에서 1씩 증가합니다. 해당 함수에 대해 드라이버에 필요한 모든 인수는 *lpszArgs* 인수에 전달된 null-terminated 문자열에 제공되어야 합니다. 이러한 기능을 제공하는 드라이버는 드라이버 관련 옵션 테이블을 유지해야 합니다. 옵션은 드라이버 설명서에 완전히 문서화되어야 합니다. 드라이버 관련 옵션을 사용하는 응용 프로그램 작성기는 이렇게 하면 응용 프로그램이 상호 운용성이 낮아집니다.  
  
### <a name="messages"></a>메시지  
 드라이버 설치 루틴은 *lpszMsg* 버퍼에서 null 종료 문자열로 응용 프로그램에 문자 메시지를 보낼 수 있습니다. 메시지가 *cbMsgMax* 문자보다 크거나 같으면 **ConfigDriver** 함수에서 null 종료 문자를 뺀 *cmsgMax로* 잘립니다.
