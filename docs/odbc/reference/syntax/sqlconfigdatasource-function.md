---
title: SQLConfig데이터 소스 함수 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299633"
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource 함수(SQLConfigDataSource Function)
**규칙**  
 버전 출시: ODBC 1.0  
  
 **요약**  
 **SQLConfigDataSource는** 데이터 원본을 추가, 수정 또는 삭제합니다.  
  
 **SQLConfigDataSource의** 기능은 ODBCCONF로 도 액세스할 수 [있습니다. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 [입력] 부모 창 핸들입니다. 핸들이 null이면 함수에 대화 상자가 표시되지 않습니다.  
  
 *f요청*  
 [입력] 요청 유형입니다. *fRequest* 인수에는 다음 값 중 하나가 포함되어야 합니다.  
  
 ODBC_ADD_DSN: 새 사용자 데이터 원본을 추가합니다.  
  
 ODBC_CONFIG_DSN: 기존 사용자 데이터 원본을 구성(수정)합니다.  
  
 ODBC_REMOVE_DSN: 기존 사용자 데이터 원본을 제거합니다.  
  
 ODBC_ADD_SYS_DSN: 새 시스템 데이터 원본을 추가합니다.  
  
 ODBC_CONFIG_SYS_DSN: 기존 시스템 데이터 원본을 수정합니다.  
  
 ODBC_REMOVE_SYS_DSN: 기존 시스템 데이터 원본을 제거합니다.  
  
 ODBC_REMOVE_DEFAULT_DSN: 시스템 정보에서 기본 데이터 원본 사양 섹션을 제거합니다. 시스템 정보의 Odbcinst.ini 항목에서 기본 드라이버 사양 섹션도 제거합니다. 이 *fRequest는* 더 이상 사용되지 제거된 **SQLRemoveDefaultDataSource** 함수와 동일한 기능을 수행합니다.) 이 옵션을 지정하면 **SQLConfigDataSource** 호출의 다른 모든 매개 변수는 NULS여야 합니다. NULL이 아닌 경우 무시됩니다.  
  
 *lpsz드라이버*  
 [입력] 실제 드라이버 이름 대신 사용자에게 표시되는 드라이버 설명(일반적으로 연결된 DBMS의 이름)입니다.  
  
 *lpsz속성*  
 [입력] 키워드-값 쌍 의 형태로 두 배로 null 종료 된 특성 목록입니다. 자세한 내용은 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)을 참조하십시오.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다. 이 함수를 호출할 때 시스템 정보에 항목이 없으면 함수는 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLConfigDataSource가 FALSE를** 반환하는 경우 **SQLInstallerError**를 호출하여 연결된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못되었습니다.|*hwndParent* 인수가 유효하지 않거나 NULL입니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못된 요청 유형|*fRequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|잘못된 드라이버 또는 번역기 이름|*lpszDriver* 인수가 잘못되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못된 키워드-값 쌍|*lpszAttributes* 인수에는 구문 오류가 포함되어 있습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|설치 프로그램이 *fRequest* 인수에서 요청한 작업을 수행할 수 없습니다. **ConfigDSN에** 대한 호출이 실패했습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 번역기 설정 라이브러리를 로드할 수 없습니다.|드라이버 설정 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLConfigDataSource는** *lpszDriver* 값을 사용하여 시스템 정보에서 드라이버에 대한 설정 DLL의 전체 경로를 읽습니다. DLL을 로드 하 고 그것에 전달 된 동일한 인수와 **ConfigDSN을** 호출 합니다.  
  
 **SQLConfigDataSource는** 설치 DLL을 찾거나 로드할 수 없거나 사용자가 대화 상자를 취소하는 경우 FALSE를 반환합니다. 그렇지 않으면 **ConfigDSN에서**받은 상태를 반환합니다.  
  
 **SQLConfigDataSource는** 시스템 DSN *fRequest*s를 사용자 DSN *fRequest*s에 매핑합니다(ODBC_ADD_DSN ODBC_ADD_SYS_DSN, ODBC_CONFIG_SYS_DSN ODBC_CONFIG_DSN, ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DSN). 사용자와 시스템 DSN을 구분하기 위해 **SQLConfigDataSource는** 다음 표에 따라 설치 관리자 구성 모드를 설정합니다. 반환하기 전에 **SQLConfigDataSource는** 구성 모드를 BOTHDSN으로 재설정합니다. **ConfigDSN(드라이버에** 의해 구현)은 시스템 DSN을 지원하기 위해 **SQLWriteDSNToIni** 및 **SQLWritePrivateProfileString을** 호출해야 합니다. 자세한 내용은 [ConfigDSN 함수를](../../../odbc/reference/syntax/configdsn-function.md)참조하십시오.  
  
|*f요청*|구성 모드|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|데이터 원본 추가, 수정 또는 제거|[구성DSN(설정](../../../odbc/reference/syntax/configdsn-function.md) DLL)|  
|시스템 정보에서 데이터 원본 이름 제거|[SQLRemoveDSNIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|시스템 정보에 데이터 원본 이름 추가|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
