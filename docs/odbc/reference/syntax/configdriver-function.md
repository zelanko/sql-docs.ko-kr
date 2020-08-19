---
description: ConfigDriver 함수
title: ConfigDriver 함수 | Microsoft Docs
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
ms.openlocfilehash: 3d59765d1b6a6a662c02b459e07bac10895838a2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428955"
---
# <a name="configdriver-function"></a>ConfigDriver 함수
**규칙**  
 소개 된 버전: ODBC 2.5  
  
 **요약**  
 **Configdriver** 를 사용 하면 프로그램에서 **ConfigDSN**를 호출 하지 않고도 설치 및 제거 기능을 수행할 수 있습니다. 이 함수는 설치 하는 동안 드라이버 관련 시스템 정보를 만들고 DSN 변환을 수행 하는 것과 같은 드라이버별 기능을 수행 하 고 제거 하는 동안 시스템 정보 수정 사항을 정리 합니다. 이 함수는 드라이버 설치 DLL 또는 별도의 설치 DLL에 의해 노출 됩니다.  
  
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
 입력 부모 창 핸들입니다. 핸들이 null 이면 함수는 대화 상자를 표시 하지 않습니다.  
  
 *fRequest*  
 입력 요청 유형입니다. *Frequest* 인수는 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_INSTALL_DRIVER: 새 드라이버를 설치 합니다.  
  
 ODBC_REMOVE_DRIVER: 드라이버를 제거 합니다.  
  
 이 옵션은 드라이버에 국한 될 수도 있습니다 .이 경우 첫 번째 옵션에 대 한 *Frequest* 인수는 ODBC_CONFIG_DRIVER_MAX + 1부터 시작 해야 합니다. 추가 옵션에 대 한 *Frequest* 인수도 ODBC_CONFIG_DRIVER_MAX + 1 보다 큰 값으로 시작 해야 합니다.  
  
 *lpszDriver*  
 입력 시스템 정보의 Odbcinst.ini 키에 등록 된 드라이버의 이름입니다.  
  
 *lpszArgs*  
 입력 드라이버별 *Frequest*에 대 한 인수를 포함 하는 null로 끝나는 문자열입니다.  
  
 *lpszMsg*  
 출력 드라이버 설정의 출력 메시지를 포함 하는 null로 끝나는 문자열입니다.  
  
 *cbMsgMax*  
 입력 *LpszMsg*의 길이입니다.  
  
 *pcbMsgOut*  
 출력 *LpszMsg*에서 반환할 수 있는 총 바이트 수입니다.  
  
 반환할 수 있는 바이트 수가 *Cbmsgmax*보다 크거나 같으면 *lpszMsg* 의 출력 메시지가 *cbmsgmax* 에서 null 종료 문자를 뺀 값으로 잘립니다. *Pcbmsgout* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **Configdriver** 가 FALSE를 반환 하면 연결 된 * \* pfErrorCode* 값이 **SQLPostInstallerError** 에 대 한 호출에 의해 설치 관리자 오류 버퍼에 게시 되 고 **SQLInstallerError**를 호출 하 여 가져올 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \* pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못 되었습니다.|*HwndParent* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못 된 요청 유형|*Frequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> 드라이버 관련 옵션이 ODBC_CONFIG_DRIVER_MAX 보다 작거나 같습니다.|  
|ODBC_ERROR_INVALID_NAME|드라이버 또는 번역기 이름이 잘못 되었습니다.|*LpszDriver* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|*Frequest* 인수에서 요청 된 작업을 수행할 수 없습니다.|  
|ODBC_ERROR_DRIVER_SPECIFIC|드라이버 또는 번역기 관련 오류|ODBC 설치 관리자 오류가 정의 되지 않은 드라이버 관련 오류입니다. **SQLPostInstallerError** 함수 호출의 *szerror* 인수는 드라이버별 오류 메시지를 포함 해야 합니다.|  
  
## <a name="comments"></a>주석  
  
### <a name="driver-specific-options"></a>드라이버 관련 옵션  
 응용 프로그램은 *Frequest* 인수를 사용 하 여 드라이버에서 제공 하는 드라이버 특정 기능을 요청할 수 있습니다. 첫 번째 옵션에 대 한 *Frequest* 는 ODBC_CONFIG_DRIVER_MAX + 1이 고 추가 옵션은 해당 값에서 1 씩 증가 합니다. 해당 함수에 대해 드라이버에 필요한 모든 인수는 *lpszArgs* 인수에 전달 된 null로 끝나는 문자열에 제공 해야 합니다. 이러한 기능을 제공 하는 드라이버는 드라이버별 옵션 테이블을 유지 해야 합니다. 이 옵션은 드라이버 설명서에 자세히 설명 되어 있습니다. 드라이버 관련 옵션을 사용 하는 응용 프로그램 작성자는 응용 프로그램의 상호 운용성을 줄여 주는 것을 인식 해야 합니다.  
  
### <a name="messages"></a>메시지  
 드라이버 설치 루틴은 *lpszMsg* 버퍼에서 null로 끝나는 문자열로 응용 프로그램에 문자 메시지를 보낼 수 있습니다. 이 메시지는 cbmsgmax가 *cbmsgmax* 문자 보다 크거나 같은 경우 **configdriver** 함수에서 null 종료 문자 *를 뺀 값* 으로 잘립니다.
