---
title: SQLConfigDataSource 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDataSource
helpviewer_keywords:
- SQLConfigDataSource function [ODBC]
ms.assetid: f8d6e342-c010-434e-b1cd-f5371fb50a14
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90a51193a8f4edbb013527c4dde0625b75131583
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299633"
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource 함수(SQLConfigDataSource Function)
**규칙**  
 소개 된 버전: ODBC 1.0  
  
 **요약**  
 **SQLConfigDataSource** 는 데이터 원본을 추가, 수정 또는 삭제 합니다.  
  
 ODBCCONF를 사용 하 여 **SQLConfigDataSource** 의 기능에 액세스할 수도 있습니다 [. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLConfigDataSource(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>인수  
 *hwndParent*  
 입력 부모 창 핸들입니다. 핸들이 null 이면 함수는 대화 상자를 표시 하지 않습니다.  
  
 *fRequest*  
 입력 요청 유형입니다. *Frequest* 인수는 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_ADD_DSN: 새 사용자 데이터 소스를 추가 합니다.  
  
 ODBC_CONFIG_DSN: 기존 사용자 데이터 원본을 구성 (수정) 합니다.  
  
 ODBC_REMOVE_DSN: 기존 사용자 데이터 원본을 제거 합니다.  
  
 ODBC_ADD_SYS_DSN: 새 시스템 데이터 소스를 추가 합니다.  
  
 ODBC_CONFIG_SYS_DSN: 기존 시스템 데이터 원본을 수정 합니다.  
  
 ODBC_REMOVE_SYS_DSN: 기존 시스템 데이터 원본을 제거 합니다.  
  
 ODBC_REMOVE_DEFAULT_DSN: 시스템 정보에서 기본 데이터 원본 사양 섹션을 제거 합니다. 또한 시스템 정보의 Odbcinst.ini 항목에서 기본 드라이버 사양 섹션을 제거 합니다. 이 *Frequest* 는 사용 되지 않는 **Sqlremovedefaultdatasource** 함수와 동일한 기능을 수행 합니다. 이 옵션을 지정 하는 경우 **SQLConfigDataSource** 에 대 한 호출의 다른 모든 매개 변수는 null 이어야 합니다. NULL이 아닌 경우 무시 됩니다.  
  
 *lpszDriver*  
 입력 실제 드라이버 이름 대신 사용자에 게 제공 되는 드라이버 설명 (일반적으로 연결 된 DBMS의 이름)입니다.  
  
 *lpszAttributes*  
 입력 키워드-값 쌍 형식으로 된 이중 null 종료 특성 목록입니다. 자세한 내용은 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)를 참조 하세요.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다. 이 함수가 호출 될 때 시스템 정보에 항목이 없으면 함수는 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLConfigDataSource** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못 되었습니다.|*HwndParent* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못 된 요청 유형|*Frequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|드라이버 또는 번역기 이름이 잘못 되었습니다.|*LpszDriver* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|*LpszAttributes* 인수에 구문 오류가 포함 되어 있습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|설치 관리자가 *Frequest* 인수에서 요청 된 작업을 수행할 수 없습니다. **ConfigDSN** 에 대 한 호출이 실패 했습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 번역기 설치 라이브러리를 로드할 수 없습니다.|드라이버 설치 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLConfigDataSource** 는 *lpszDriver* 값을 사용 하 여 시스템 정보에서 드라이버에 대 한 설치 DLL의 전체 경로를 읽습니다. DLL을 로드 하 고 전달 된 것과 동일한 인수를 사용 하 여 **ConfigDSN** 를 호출 합니다.  
  
 **SQLConfigDataSource** 는 설치 DLL을 찾거나 로드할 수 없거나 사용자가 대화 상자를 취소 한 경우 FALSE를 반환 합니다. 그렇지 않으면 **ConfigDSN**에서 받은 상태를 반환 합니다.  
  
 **SQLConfigDataSource** 시스템 Dsn *Frequest*s를 *사용자 DSN frequest s에*매핑합니다 (ODBC_ADD_SYS_DSN ODBC_ADD_DSN, ODBC_CONFIG_DSN ODBC_CONFIG_SYS_DSN 하 고 ODBC_REMOVE_SYS_DSN). 사용자 및 시스템 Dsn을 구분 하기 위해 **SQLConfigDataSource** 는 다음 표에 따라 설치 관리자 구성 모드를 설정 합니다. 을 반환 하기 전에 **SQLConfigDataSource** 는 구성 모드를 BOTHDSN로 다시 설정 합니다. **ConfigDSN** (드라이버에서 구현)는 **Sqlwritedsntoini** 및 **SQLWritePrivateProfileString** 를 호출 하 여 시스템 DSN을 지원 해야 합니다. 자세한 내용은 [ConfigDSN 함수](../../../odbc/reference/syntax/configdsn-function.md)를 참조 하세요.  
  
|*fRequest*|구성 모드|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|데이터 원본 추가, 수정 또는 제거|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (설치 DLL)|  
|시스템 정보에서 데이터 원본 이름 제거|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|시스템 정보에 데이터 원본 이름 추가|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
