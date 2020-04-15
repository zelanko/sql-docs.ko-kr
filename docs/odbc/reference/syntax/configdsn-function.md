---
title: ConfigDSN 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDSN
helpviewer_keywords:
- ConfigDSN [ODBC]
ms.assetid: 01ced74e-c575-4a25-83f5-bd7d918123f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbae126c819088bd277621b207454503a86c8955
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306044"
---
# <a name="configdsn-function"></a>ConfigDSN 함수
**규칙**  
 버전 출시: ODBC 1.0  
  
 **요약**  
 **ConfigDSN은** 시스템 정보에서 데이터 원본을 추가, 수정 또는 삭제합니다. 연결 정보를 묻는 메시지가 표시될 수 있습니다. 드라이버 DLL 또는 별도의 설치 DLL에 있을 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL ConfigDSN(  
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
  
 ODBC_ADD_DSN: 새 데이터 원본을 추가합니다.  
  
 ODBC_CONFIG_DSN: 기존 데이터 원본을 구성(수정)합니다.  
  
 ODBC_REMOVE_DSN: 기존 데이터 원본을 제거합니다.  
  
 *lpsz드라이버*  
 [입력] 실제 드라이버 이름 대신 사용자에게 표시되는 드라이버 설명(일반적으로 연결된 DBMS의 이름)입니다.  
  
 *lpsz속성*  
 [입력] 키워드-값 쌍 의 형태로 두 배로 null 종료 된 특성 목록입니다. 자세한 내용은 '댓글'을 참조하세요.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **ConfigDSN이 FALSE를** 반환하면 연결된 * \*pfErrorCode* 값이 **SQLPostInstallerError** 호출을 통해 설치 관리자 오류 버퍼에 게시되며 **SQLInstaller Error를**호출하여 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못되었습니다.|*hwndParent* 인수가 잘못되었습니다.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못된 키워드-값 쌍|*lpszAttributes* 인수에는 구문 오류가 포함되어 있습니다.|  
|ODBC_ERROR_INVALID_NAME|잘못된 드라이버 또는 번역기 이름|*lpszDriver* 인수가 잘못되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못된 요청 유형|*fRequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|*fRequest* 인수에서 요청한 작업을 수행할 수 없습니다.|  
|ODBC_ERROR_DRIVER_SPECIFIC|드라이버 또는 번역기 관련 오류|정의된 ODBC 설치 관리자 오류가 없는 드라이버별 오류입니다. **SQLPostInstallerError** 함수에 대 한 호출에서 *SzError* 인수 드라이버 관련 오류 메시지를 포함 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **ConfigDSN은** 키어드 값 쌍의 형태로 특성 목록으로 설치 관리자 DLL에서 연결 정보를 받습니다. 각 쌍은 null 바이트로 종료되고 전체 목록은 null 바이트로 종료됩니다. 즉, 두 개의 null 바이트가 목록의 끝을 표시합니다. 키워드 값 쌍의 등호 주위에 공백은 허용되지 않습니다. **ConfigDSN은** **SQLBrowseConnect** 및 **SQLDriverConnect에**대한 유효한 키워드가 아닌 키워드를 허용할 수 있습니다. **ConfigDSN은** **SQLBrowseConnect** 및 **SQLDriverConnect**에 대한 유효한 키워드인 모든 키워드를 반드시 지원하지는 않습니다. **(configDSN은** **DRIVER** 키워드를 허용하지 않습니다.) **ConfigDSN** 함수에서 사용하는 키워드는 설치 프로그램의 AUTO 설치 기능을 사용하여 데이터 원본을 다시 만드는 데 필요한 모든 옵션을 지원해야 합니다. **ConfigDSN** 값과 연결 문자열 값의 사용이 동일한 경우 동일한 키워드를 사용해야 합니다.  
  
 **SQLBrowseConnect** 및 **SQLDriverConnect에서와**같이 키워드와 해당 값은 **[]{}(;)를 포함해서는 안됩니다. \*=!@문자및** **DSN** 키워드의 값은 공백으로만 구성될 수 없습니다. 레지스트리 문법으로 인해 키워드 및 데이터 원본 이름은 백슬래시()\\문자를 포함할 수 없습니다.  
  
 **ConfigDSN은** **SQLValidDSN을** 호출하여 데이터 원본 이름의 길이를 확인하고 잘못된 문자가 이름에 포함되지 않았는지 확인해야 합니다. 데이터 원본 이름이 SQL_MAX_DSN_LENGTH 이상이거나 잘못된 문자를 포함하는 경우 **SQLValidDSN은** 오류를 반환하고 **ConfigDSN은** 오류를 반환합니다. 데이터 원본 이름의 길이도 **SQLWriteDSNToIni**.  
  
 예를 들어 사용자 ID, 암호 및 데이터베이스 이름이 필요한 데이터 원본을 구성하려면 설치 응용 프로그램이 다음 키워드 값 쌍을 전달할 수 있습니다.  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 이러한 키워드에 대한 자세한 내용은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 및 각 드라이버 설명서를 참조하십시오.  
  
 대화 상자를 표시하려면 *hwndParent가* null이 아니어야 합니다.  
  
## <a name="adding-a-data-source"></a>데이터 원본 추가  
 데이터 원본 이름이 *lpszAttributes에서* **ConfigDSN에** 전달되는 경우 **ConfigDSN은** 이름이 유효한지 확인합니다. 데이터 원본 이름이 기존 데이터 원본 이름과 일치하고 *hwndParent가* null인 경우 **ConfigDSN은** 기존 이름을 덮어씁니다. 기존 이름과 일치하고 *hwndParent가* null이 아닌 경우 **ConfigDSN은** 사용자에게 기존 이름을 덮어쓰라는 메시지를 표시합니다.  
  
 *lpszAttributes가* 데이터 원본에 연결하기에 충분한 정보가 포함되어 있는 경우 **ConfigDSN은** 데이터 원본을 추가하거나 사용자가 연결 정보를 변경할 수 있는 대화 상자를 표시할 수 있습니다. *lpszAttribute가* 데이터 원본에 연결하기에 충분한 정보가 없는 경우 **ConfigDSN은** 필요한 정보를 결정해야 합니다. *hwndParent가* null이 아닌 경우 사용자로부터 정보를 검색하는 대화 상자가 표시됩니다.  
  
 **ConfigDSN이** 대화 상자를 표시하는 경우 대화 상자에 전달된 연결 정보를 *lpszAttributes로*표시해야 합니다. 특히 데이터 원본 이름이 전달된 경우 **ConfigDSN은** 해당 이름을 표시하지만 사용자가 변경할 수 없습니다. **ConfigDSN은** *lpszAttribute에서*전달되지 않은 연결 정보에 대한 기본값을 제공할 수 있습니다.  
  
 **ConfigDSN이** 데이터 원본에 대한 전체 연결 정보를 얻을 수 없는 경우 FALSE를 반환합니다.  
  
 **ConfigDSN이** 데이터 원본에 대한 완전한 연결 정보를 얻을 수 있는 경우 설치 관리자 DLL에서 **SQLWriteDSNToIni를** 호출하여 Odbc.ini 파일(또는 레지스트리)에 새 데이터 원본 사양을 추가합니다. **SQLWriteDSNToIni는** [ODBC 데이터 원본] 섹션에 데이터 원본 이름을 추가하고 데이터 원본 사양 섹션을 만들고 드라이버 설명과 함께 **DRIVER** 키워드를 해당 값으로 추가합니다. **ConfigDSN은** 설치 관리자 DLL에서 **SQLWritePrivateProfileString을** 호출하여 드라이버에서 사용하는 추가 키워드와 값을 추가합니다.  
  
## <a name="modifying-a-data-source"></a>데이터 원본 수정  
 데이터 원본을 수정하려면 데이터 원본 이름을 *lpszAttribute에서* **ConfigDSN에** 전달해야 합니다. **ConfigDSN은** 데이터 원본 이름이 Odbc.ini 파일(또는 레지스트리)에 있는지 확인합니다.  
  
 *hwndParent가* null인 경우 **ConfigDSN은** *lpszAttributes의* 정보를 사용하여 Odbc.ini 파일(또는 레지스트리)의 정보를 수정합니다. *hwndParent가* null이 아닌 경우 **ConfigDSN은** *lpszAttributes의*정보를 사용하여 대화 상자를 표시합니다. *lpszAttributes에*없는 정보에 대 한 시스템 정보의 정보를 사용 합니다. 사용자는 **ConfigDSN이** 시스템 정보에 정보를 저장하기 전에 정보를 수정할 수 있습니다.  
  
 데이터 원본 이름이 변경된 경우 **ConfigDSN은** 먼저 설치 프로그램 DLL에서 **SQLRemoveDSNFromIni를** 호출하여 Odbc.ini 파일(또는 레지스트리)에서 기존 데이터 원본 사양을 제거합니다. 그런 다음 이전 섹션의 단계를 수행하여 새 데이터 원본 사양을 추가합니다. 데이터 원본 이름이 변경되지 않은 경우 **ConfigDSN은** 설치 관리자 DLL에서 **SQLWritePrivateProfileString을** 호출하여 다른 변경 사항을 만듭니다. **ConfigDSN은** **드라이버** 키워드의 값을 삭제하거나 변경할 수 없습니다.  
  
## <a name="deleting-a-data-source"></a>데이터 원본 삭제  
 데이터 원본을 삭제하려면 데이터 원본 이름을 *lpszAttribute의* **ConfigDSN에** 전달해야 합니다. **ConfigDSN은** 데이터 원본 이름이 Odbc.ini 파일(또는 레지스트리)에 있는지 확인합니다. 그런 다음 설치 프로그램 DLL에서 **SQLRemoveDSNFromIni를** 호출하여 데이터 원본을 제거합니다.  
  
## <a name="note"></a>참고
 이 루틴의 유니코드 버전을 작성하는 경우 LPCSTR 대신 LPCWSTR 인수를 통해 **ConfigDSNW라고**해야 합니다.
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|데이터 원본 추가, 수정 또는 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Odbc.ini 파일 또는 레지스트리에서 값 얻기|[SQLGet개인 프로필 스트링](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|기본 데이터 원본 제거|[SQLRemoveDefault데이터 소스](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Odbc.ini(또는 레지스트리)에서 데이터 원본 이름 제거|[SQLRemoveDSNIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Odbc.ini(또는 레지스트리)에 데이터 원본 이름 추가|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Odbc.ini 파일 또는 레지스트리에 값 쓰기|[SQLWrite개인 프로필 스트링](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
