---
title: ConfigDSN 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 78be24ea75fad04c7b7c1bdae103dfd3f92c78ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016721"
---
# <a name="configdsn-function"></a>ConfigDSN 함수
**규칙**  
 도입 된 버전: ODBC 1.0  
  
 **요약**  
 **ConfigDSN** 추가, 수정 또는 시스템 정보에서 데이터 원본을 삭제 합니다. 연결 정보에 대 한 사용자 라는 메시지가 나타납니다. 드라이버 DLL 또는 별도 설치 프로그램 DLL 수 있습니다.  
  
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
 [입력] 부모 창 핸들입니다. 핸들을 null 이면 함수는 모든 대화 상자 표시 되지 않습니다.  
  
 *fRequest*  
 [입력] 요청 유형입니다. 합니다 *문제점과* 인수는 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_ADD_DSN: 새 데이터 원본을 추가 합니다.  
  
 ODBC_CONFIG_DSN: 구성 (수정) 기존 데이터 원본입니다.  
  
 ODBC_REMOVE_DSN: 기존 데이터 원본을 제거 합니다.  
  
 *lpszDriver*  
 [입력] 드라이버 설명 (일반적으로 연결된 되는 DBMS의 이름) 실제 드라이버 이름 대신 사용자에 게 표시 합니다.  
  
 *lpszAttributes*  
 [입력] 키워드-값 쌍의 형태로 특성 목록을 이중 null로 종료 합니다. 자세한 내용은 "설명입니다."을 참조 하세요.  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **ConfigDSN** 연결 된 FALSE를 반환  *\*pfErrorCode* 값을 호출 하 여 설치 관리자 오류 버퍼에 게시 됩니다 **SQLPostInstallerError** 및 호출 하 여 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|잘못 된 창 핸들|합니다 *hwndParent* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|합니다 *lpszAttributes* 인수 구문 오류를 포함 합니다.|  
|ODBC_ERROR_INVALID_NAME|잘못 된 드라이버 또는 변환기 이름|합니다 *lpszDriver* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|합니다 *문제점과* 인수 중 하나 였습니다.<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|요청한 작업을 수행할 수 없습니다는 *문제점과* 인수입니다.|  
|ODBC_ERROR_DRIVER_SPECIFIC|드라이버 또는 translator 관련 오류|정의 된 ODBC 설치 관리자 오류가 없는 드라이버 관련 오류가 발생 했습니다. 합니다 *SzError* 호출에서 인수를 **SQLPostInstallerError** 함수 드라이버 관련 오류 메시지를 포함 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **ConfigDSN** 키워드-값 쌍의 형태로 특성의 목록으로 설치 관리자 DLL에서에서 연결 정보를 받습니다. 각 쌍을 null 바이트를 사용 하 여 종료 됩니다 하 고 전체 목록을 null 바이트를 사용 하 여 종료 됩니다. (즉, 두 개의 null 바이트의 끝을 표시 목록입니다.) 키워드-값 쌍에서 등호 앞뒤 공백은 허용 되지 않습니다. **ConfigDSN** 에 대 한 유효한 키워드 없는 키워드를 사용할 수 있습니다 **SQLBrowseConnect** 하 고 **SQLDriverConnect**합니다. **ConfigDSN** 반드시 지원에 대 한 유효한 키워드는 모든 키워드 **SQLBrowseConnect** 하 고 **SQLDriverConnect**합니다. (**ConfigDSN** 받아들이지 않는 합니다 **드라이버** 키워드입니다.) 사용 된 키워드를 **ConfigDSN** 함수 설치 관리자의 자동 설치 기능을 사용 하 여 데이터 소스를 다시 만드는 데 필요한 모든 옵션을 지원 해야 합니다. 때 사용 합니다 **ConfigDSN** 값 및 연결 문자열 값은 동일 같은 키워드를 사용 해야 합니다.  
  
 에서처럼 **SQLBrowseConnect** 및 **SQLDriverConnect**, 키워드 및 해당 값 포함 하지 않아야 합니다 **{}(),? \*=! @** 문자 및 값을 **DSN** 키워드 공백으로 구성 될 수 없습니다. 레지스트리 문법으로 인해 키워드 및 데이터 원본 이름은 백슬래시를 포함할 수 없습니다 (\\) 문자입니다.  
  
 **ConfigDSN** 를 호출 해야 **SQLValidDSN** 데이터 원본 이름의 길이 확인 하 고 이름에 잘못 된 문자 포함 되어 있는지 확인 합니다. 데이터 원본 이름을 SQL_MAX_DSN_LENGTH 보다 오래 되었거나 잘못 된 문자를 포함 하는 경우 **SQLValidDSN** 오류를 반환 하 고 **ConfigDSN** 오류를 반환 합니다. 데이터 원본 이름의 길이도 여 확인란이 **SQLWriteDSNToIni**합니다.  
  
 예를 들어 사용자 ID, 암호 및 데이터베이스 이름이 필요 하는 데이터 소스를 구성 하려면 설치 응용 프로그램을 다음 키워드-값 쌍을 전달 될 수 있습니다.  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 이러한 키워드에 대 한 자세한 내용은 참조 하세요. [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 및 각 드라이버의 설명서.  
  
 대화 상자를 표시할 *hwndParent* null이 아니어야 합니다.  
  
## <a name="adding-a-data-source"></a>데이터 소스 추가  
 데이터 원본 이름에 전달 되 면 **ConfigDSN** 에 *lpszAttributes*합니다 **ConfigDSN** 이름이 올바른지 확인 합니다. 데이터 원본 이름은 기존 데이터 원본 이름과 일치 하는 경우 및 *hwndParent* 가 null **ConfigDSN** 기존 이름을 덮어씁니다. 기존 이름과 일치 하는 경우 및 *hwndParent* null이 아니면 **ConfigDSN** 기존 이름을 덮어쓰지 하 라는 메시지를 표시 합니다.  
  
 하는 경우 *lpszAttributes* 데이터 원본에 연결할 정보가 충분히 포함 된 **ConfigDSN** 데이터 원본 또는 사용자 연결 정보를 변경할 수 있는 대화 상자를 표시에 추가할 수 있습니다. 하는 경우 *lpszAttributes* 데이터 원본에 연결 하려면 충분 한 정보를 포함 하지 **ConfigDSN** 하는 경우 필요한 정보를 확인 해야 합니다 *hwndParent* null이 아니면 사용자 로부터 정보를 검색 하는 대화 상자가 표시 됩니다.  
  
 하는 경우 **ConfigDSN** 대화 상자를 표시에 전달 되는 모든 연결 정보를 표시 해야 할 *lpszAttributes*합니다. 특히, 데이터 원본 이름에 전달한 **ConfigDSN** 해당 이름을 표시 하지만 사용자가 변경할 것을 허용 하지 않습니다. **ConfigDSN** 에 전달 되지 연결 정보에 대 한 기본값을 제공할 수 있습니다 *lpszAttributes*합니다.  
  
 하는 경우 **ConfigDSN** 전체 연결 정보를 가져올 수 없습니다. 데이터 원본에 대해 FALSE를 반환 합니다.  
  
 하는 경우 **ConfigDSN** 데이터 원본에 대 한 전체 연결 정보를 얻을 수, 호출 **SQLWriteDSNToIni** DLL Odbc.ini 파일 (또는 레지스트리)에 새 데이터 원본 사양에 추가할 설치 관리자에서. **SQLWriteDSNToIni** 데이터 원본 이름 [ODBC 데이터 소스] 섹션에 추가 하는 데이터 원본 사양 섹션을 만들고 추가 합니다 **드라이버** 키워드를 값으로 드라이버 설명 합니다. **ConfigDSN** 호출 **SQLWritePrivateProfileString** 설치 관리자 DLL이 추가 키워드 및 드라이버에서 사용 되는 값을 추가 합니다.  
  
## <a name="modifying-a-data-source"></a>데이터 원본 수정  
 데이터 소스를 수정 하려면 데이터 원본 이름으로 전달 해야 **ConfigDSN** 에 *lpszAttributes*합니다. **ConfigDSN** Odbc.ini 파일 (또는 레지스트리)에서 데이터 원본 이름 인지 확인 합니다.  
  
 경우 *hwndParent* 가 null **ConfigDSN** 의 정보를 사용 하 여 *lpszAttributes* Odbc.ini 파일 (또는 레지스트리)에 대 한 정보를 수정할 수 있습니다. 하는 경우 *hwndParent* null이 아니면 **ConfigDSN** 의 정보를 사용 하 여 대화 상자를 표시 *lpszAttributes*;에 없는 정보에 대 한 *lpszAttributes* , 정보 시스템 정보를 사용 합니다. 사용자가 하기 전에 정보를 수정할 수 **ConfigDSN** 시스템 정보에 저장 합니다.  
  
 데이터 원본 이름이 변경 된 경우 **ConfigDSN** 는 먼저 호출 **SQLRemoveDSNFromIni** 설치 관리자에서 기존 데이터를 제거 하는 DLL 원본 Odbc.ini 파일 (또는 레지스트리에서) 사양입니다. 그런 다음 새 데이터 원본을 지정을 추가 하려면 이전 섹션의 단계를 따릅니다. 데이터 원본 이름은 변경 되지 않았습니다 하는 경우 **ConfigDSN** 호출 **SQLWritePrivateProfileString** 설치 관리자 DLL이 다른 변경을 수행 합니다. **ConfigDSN** 삭제 하거나 값을 변경할 수는 **드라이버** 키워드입니다.  
  
## <a name="deleting-a-data-source"></a>데이터 원본 삭제  
 데이터 소스를 삭제 하려면 데이터 원본 이름으로 전달 해야 **ConfigDSN** 에 *lpszAttributes*합니다. **ConfigDSN** Odbc.ini 파일 (또는 레지스트리)에서 데이터 원본 이름 인지 확인 합니다. 그런 다음 호출 **SQLRemoveDSNFromIni** 설치 관리자 DLL이 데이터 원본을 제거 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 데이터 원본 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Odbc.ini 파일 또는 레지스트리에서 값 가져오기|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|기본 데이터 원본 제거|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Odbc.ini (또는 레지스트리)에서 데이터 원본 이름 제거|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|데이터 원본 이름을 Odbc.ini (또는 레지스트리)에 추가|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Odbc.ini 파일 또는 레지스트리 값을 쓰는|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
