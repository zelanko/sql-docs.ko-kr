---
title: "ConfigDriver 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: ConfigDriver
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: ConfigDriver
helpviewer_keywords: ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1697b7e697760afee2b62c49bd24c2ab22c9201d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="configdriver-function"></a>ConfigDriver 함수
**규칙**  
 2.5 ODBC에 도입 된 버전:  
  
 **요약**  
 **ConfigDriver** 설치를 수행 하 고 프로그램을 호출할 필요 없이 함수를 제거 하는 설치 프로그램을 사용 하면 **ConfigDSN**합니다. 이 함수는 드라이버 관련 시스템 정보를 만드는 및 DSN 변환을 수행 하 고 설치 하는 동안으로 제거 하는 동안 시스템 정보 수정 정리 같은 드라이버별 함수를 수행 합니다. 이 함수는 드라이버 설치 DLL 또는 별도 설치 DLL에 의해 노출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 *창은*  
 [입력] 부모 창 핸들입니다. 핸들 null 이면 함수는 모든 대화 상자 표시 되지 않습니다.  
  
 *문제점과*  
 [입력] 요청의 유형입니다. *문제점과* 인수는 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_INSTALL_DRIVER: 새 드라이버를 설치 합니다.  
  
 ODBC_REMOVE_DRIVER: 드라이버를 제거 합니다.  
  
 이 옵션 또한 수 드라이버 관련은 쿼리에서 *문제점과* 첫 번째 옵션에 대 한 인수 ODBC_CONFIG_DRIVER_MAX + 1에서 시작 해야 합니다. *문제점과* 추가 옵션에 대 한 인수 ODBC_CONFIG_DRIVER_MAX + 1 보다 큰 값에서 시작 해야 합니다.  
  
 *lpszDriver*  
 [입력] 시스템 정보 Odbcinst.ini 키에 등록 하는 드라이버의 이름입니다.  
  
 *lpszArgs*  
 [입력] 드라이버 관련에 대 한 인수를 포함 하는 null로 끝나는 문자열 *문제점과*합니다.  
  
 *lpszMsg*  
 [출력] 드라이버 설치 프로그램에서 출력 메시지를 포함 하는 null로 끝나는 문자열입니다.  
  
 *cbMsgMax*  
 [입력] 길이 *lpszMsg*합니다.  
  
 *pcbMsgOut*  
 [출력] 반환 하려면 사용 가능한 바이트의 총 수 *lpszMsg*합니다.  
  
 보다 크거나 반환에 사용할 수 있는 바이트 수가 *cbMsgMax*, 출력 메시지에 *lpszMsg* 잘립니다 *cbMsgMax* 뺀 null 종료 문자입니다. *pcbMsgOut* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **ConfigDriver** 관련 FALSE를 반환  *\*pfErrorCode* 를 호출 하 여 설치 관리자 오류 버퍼에 값이 게시 **SQLPostInstallerError** 호출 하 여 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|잘못 된 창 핸들|*창은* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|*문제점과* 인수는 다음 중 하나 였습니다.<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> 드라이버 관련 옵션 ODBC_CONFIG_DRIVER_MAX 보다 작거나 했습니다.|  
|ODBC_ERROR_INVALID_NAME|잘못 된 드라이버 또는 변환기 이름입니다.|*lpszDriver* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|요청한 작업을 수행할 수 없습니다는 *문제점과* 인수입니다.|  
|ODBC_ERROR_DRIVER_SPECIFIC|드라이버 또는 변환기 관련 오류|정의 된 ODBC 설치 관리자 오류가 없는 드라이버 관련 오류가 발생 했습니다. *SzError* 에 대 한 호출의 인수는 **SQLPostInstallerError** 함수에는 드라이버 특정 오류 메시지가 포함 되어 있어야 합니다.|  
  
## <a name="comments"></a>주석  
  
### <a name="driver-specific-options"></a>드라이버 관련 옵션  
 응용 프로그램 사용 하 여 드라이버에 의해 노출 되는 드라이버 관련 기능을 요청할 수는 *문제점과* 인수입니다. *문제점과* 첫 번째 옵션 1을 더한 ODBC_CONFIG_DRIVER_MAX 됩니다 및 추가 옵션을 해당 값에서 1 씩 증가 합니다. 전달 된 null로 끝나는 문자열에 제공 해야 해당 함수에 대 한 드라이버에 필요한 모든 인수는 *lpszArgs* 인수입니다. 이러한 기능을 제공 하는 드라이버는 드라이버 관련 옵션의 테이블을 유지 해야 합니다. 옵션은 드라이버 설명서의 완전히 문서화 해야 합니다. 드라이버 관련 옵션을 사용 하는 응용 프로그램 작성자는 이렇게 하면 응용 프로그램 덜 상호 운용 가능한 알고 있어야 합니다.  
  
### <a name="messages"></a>메시지  
 드라이버 설치 루틴에서 null로 끝나는 문자열로 응용 프로그램에 문자 메시지를 보낼 수는 *lpszMsg* 버퍼입니다. 메시지가 잘릴 수 *cbMsgMax* 뺀 하 여 null 종결 문자는 **ConfigDriver** 보다 크거나 같은 경우에 작동 *cbMsgMax* 문자입니다.
