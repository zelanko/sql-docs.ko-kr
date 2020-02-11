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
ms.openlocfilehash: 21a02107359b26c0dc30aa87acbf46c1ab1a172d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892855"
---
# <a name="configdsn-function"></a>ConfigDSN 함수
**규칙**  
 소개 된 버전: ODBC 1.0  
  
 **요약**  
 **ConfigDSN** 는 시스템 정보에서 데이터 원본을 추가, 수정 또는 삭제 합니다. 사용자에 게 연결 정보를 입력 하 라는 메시지가 표시 될 수 있습니다. 드라이버 DLL 또는 별도의 설치 DLL에 있을 수 있습니다.  
  
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
 입력 부모 창 핸들입니다. 핸들이 null 이면 함수는 대화 상자를 표시 하지 않습니다.  
  
 *fRequest*  
 입력 요청 유형입니다. *Frequest* 인수는 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_ADD_DSN: 새 데이터 원본을 추가 합니다.  
  
 ODBC_CONFIG_DSN: 기존 데이터 원본을 구성 (수정) 합니다.  
  
 ODBC_REMOVE_DSN: 기존 데이터 원본을 제거 합니다.  
  
 *lpszDriver*  
 입력 실제 드라이버 이름 대신 사용자에 게 제공 되는 드라이버 설명 (일반적으로 연결 된 DBMS의 이름)입니다.  
  
 *lpszAttributes*  
 입력 키워드-값 쌍 형식으로 된 이중 null 종료 특성 목록입니다. 자세한 내용은 "설명"을 참조 하십시오.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **ConfigDSN** 가 FALSE를 반환 하는 * \** 경우 연결 된 pfErrorCode 값은 **SQLPostInstallerError** 를 호출 하 여 설치 관리자 오류 버퍼에 게시 되며 **SQLInstallerError**를 호출 하 여 가져올 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|창 핸들이 잘못 되었습니다.|*HwndParent* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|*LpszAttributes* 인수에 구문 오류가 포함 되어 있습니다.|  
|ODBC_ERROR_INVALID_NAME|드라이버 또는 번역기 이름이 잘못 되었습니다.|*LpszDriver* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못 된 요청 유형|*Frequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|*Frequest* 인수에서 요청 된 작업을 수행할 수 없습니다.|  
|ODBC_ERROR_DRIVER_SPECIFIC|드라이버 또는 번역기 관련 오류|ODBC 설치 관리자 오류가 정의 되지 않은 드라이버 관련 오류입니다. **SQLPostInstallerError** 함수 호출의 *szerror* 인수는 드라이버별 오류 메시지를 포함 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **ConfigDSN** 는 설치 관리자 DLL에서 키워드-값 쌍 형식의 특성 목록으로 연결 정보를 받습니다. 각 쌍은 null 바이트로 종료 되며 전체 목록이 null 바이트로 종료 됩니다. 즉, 두 개의 null 바이트가 목록의 끝을 표시 합니다. 키워드-값 쌍의 등호 앞뒤에는 공백을 사용할 수 없습니다. **ConfigDSN** 는 **SQLBrowseConnect** 및 **SQLDriverConnect**에 대 한 유효한 키워드가 아닌 키워드를 사용할 수 있습니다. **ConfigDSN** 는 **SQLBrowseConnect** 및 **SQLDriverConnect**에 대 한 유효한 키워드인 키워드를 반드시 지원 하지는 않습니다. **ConfigDSN** 은 **DRIVER** 키워드를 허용 하지 않습니다. **ConfigDSN** 함수에서 사용 되는 키워드는 설치 관리자의 자동 설정 기능을 사용 하 여 데이터 원본을 다시 만드는 데 필요한 모든 옵션을 지원 해야 합니다. **ConfigDSN** 값을 사용 하 고 연결 문자열 값이 같으면 동일한 키워드를 사용 해야 합니다.  
  
 **SQLBrowseConnect** 및 **SQLDriverConnect**에서와 같이 키워드와 해당 값은 **[]{}(),;?를 포함 하지 않아야 합니다. = \*! @** 문자 및 **DSN** 키워드 값은 공백으로만 구성 될 수 없습니다. 레지스트리 문법 때문에 키워드와 데이터 원본 이름에는 백슬래시 (\\) 문자를 사용할 수 없습니다.  
  
 **ConfigDSN** 는 **sqlinvalid dsn** 을 호출 하 여 데이터 원본 이름의 길이를 확인 하 고 이름에 잘못 된 문자가 포함 되어 있지 않은지 확인 해야 합니다. 데이터 원본 이름이 SQL_MAX_DSN_LENGTH 보다 길거나 잘못 된 문자를 포함 하는 경우 **Sqlinvalid DSN** 은 오류를 반환 하 고 **ConfigDSN** 는 오류를 반환 합니다. 또한 데이터 원본 이름의 길이는 **Sqlwritedsntoini**에 의해 확인 됩니다.  
  
 예를 들어 사용자 ID, 암호 및 데이터베이스 이름이 필요한 데이터 원본을 구성 하기 위해 설치 응용 프로그램에서 다음과 같은 키워드-값 쌍을 전달할 수 있습니다.  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 이러한 키워드에 대 한 자세한 내용은 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 및 각 드라이버의 설명서를 참조 하세요.  
  
 대화 상자를 표시 하려면 *hwndParent* 가 null이 아니어야 합니다.  
  
## <a name="adding-a-data-source"></a>데이터 원본 추가  
 데이터 원본 이름이 *lpszAttributes*의 **ConfigDSN** 에 전달 되는 경우 **ConfigDSN** 는 이름이 유효한 지 확인 합니다. 데이터 원본 이름이 기존 데이터 원본 이름과 일치 하 고 *hwndParent* 가 Null 이면 **ConfigDSN** 는 기존 이름을 덮어씁니다. 기존 이름과 일치 하 고 *hwndParent* 가 null이 아닌 경우 **ConfigDSN** 는 사용자에 게 기존 이름을 덮어쓸지 묻는 메시지를 표시 합니다.  
  
 *LpszAttributes* 데이터 원본에 연결 하는 데 충분 한 정보를 포함 하는 경우 **ConfigDSN** 는 데이터 원본을 추가 하거나 사용자가 연결 정보를 변경할 수 있는 대화 상자를 표시할 수 있습니다. *LpszAttributes* 데이터 원본에 연결 하는 데 충분 한 정보를 포함 하지 않는 경우 **ConfigDSN** 는 필요한 정보를 결정 해야 합니다. *hwndParent* 가 null이 아닌 경우 사용자 로부터 정보를 검색할 수 있는 대화 상자가 표시 됩니다.  
  
 **ConfigDSN** 에서 대화 상자를 표시 하는 경우 *lpszAttributes*에 전달 된 연결 정보를 표시 해야 합니다. 특히 데이터 원본 이름이 전달 된 경우 **ConfigDSN** 는 해당 이름을 표시 하지만 사용자가 변경할 수는 없습니다. **ConfigDSN** 는 *lpszAttributes*에서 전달 되지 않는 연결 정보에 대 한 기본값을 제공할 수 있습니다.  
  
 **ConfigDSN** 가 데이터 원본에 대 한 전체 연결 정보를 가져올 수 없는 경우 FALSE를 반환 합니다.  
  
 **ConfigDSN** 가 데이터 원본에 대 한 전체 연결 정보를 가져올 수 있는 경우 설치 관리자 DLL에서 **Sqlwritedsntoini** 를 호출 하 여 새 데이터 원본 사양을 Odbc .ini 파일 (또는 레지스트리)에 추가 합니다. **Sqlwritedsntoini** 는 [ODBC 데이터 원본] 섹션에 데이터 원본 이름을 추가 하 고 데이터 원본 사양 섹션을 만든 다음 드라이버 설명을 해당 값으로 사용 하 여 **driver** 키워드를 추가 합니다. **ConfigDSN** 는 설치 관리자 DLL의 **SQLWritePrivateProfileString** 를 호출 하 여 드라이버에서 사용 하는 추가 키워드 및 값을 추가 합니다.  
  
## <a name="modifying-a-data-source"></a>데이터 원본 수정  
 데이터 원본을 수정 하려면 데이터 원본 이름을 *lpszAttributes*의 **ConfigDSN** 에 전달 해야 합니다. **ConfigDSN** 는 데이터 원본 이름이 Odbc .ini 파일 (또는 레지스트리)에 있는지 확인 합니다.  
  
 *HwndParent* 가 null 인 경우 **ConfigDSN** 는 *lpszAttributes* 의 정보를 사용 하 여 Odbc .ini 파일 (또는 레지스트리)의 정보를 수정 합니다. *HwndParent* 가 null이 아닌 경우 **ConfigDSN** 는 *lpszAttributes*의 정보를 사용 하 여 대화 상자를 표시 합니다. *lpszAttributes*에 없는 정보는 시스템 정보의 정보를 사용 합니다. **ConfigDSN** 가 시스템 정보에 저장 하기 전에 사용자가 정보를 수정할 수 있습니다.  
  
 데이터 원본 이름이 변경 된 경우 **ConfigDSN** 는 먼저 설치 관리자 DLL의 **SQLRemoveDSNFromIni** 를 호출 하 여 Odbc .ini 파일 (또는 레지스트리)에서 기존 데이터 원본 사양을 제거 합니다. 그런 다음 이전 섹션의 단계에 따라 새 데이터 원본 사양을 추가 합니다. 데이터 원본 이름이 변경 되지 않은 경우 **ConfigDSN** 는 설치 관리자 DLL의 **SQLWritePrivateProfileString** 를 호출 하 여 다른 변경을 수행 합니다. **ConfigDSN** 은 **Driver** 키워드의 값을 삭제 하거나 변경할 수 없습니다.  
  
## <a name="deleting-a-data-source"></a>데이터 원본 삭제  
 데이터 원본을 삭제 하려면 데이터 원본 이름을 *lpszAttributes*의 **ConfigDSN** 에 전달 해야 합니다. **ConfigDSN** 는 데이터 원본 이름이 Odbc .ini 파일 (또는 레지스트리)에 있는지 확인 합니다. 그런 다음 설치 관리자 DLL에서 **SQLRemoveDSNFromIni** 를 호출 하 여 데이터 원본을 제거 합니다.  
  
## <a name="note"></a>참고
 이 루틴의 유니코드 버전을 작성 하는 경우 LPCSTR 대신 LPCWSTR 인수를 사용 하 여 **ConfigDSNW**를 호출 해야 합니다.
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|데이터 원본 추가, 수정 또는 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Odbc .ini 파일 또는 레지스트리에서 값 가져오기|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|기본 데이터 소스 제거|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Odbc .ini (또는 레지스트리에서)에서 데이터 원본 이름 제거|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Odbc .ini (또는 레지스트리에 데이터 원본 이름) 추가|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Odbc .ini 파일 또는 레지스트리에 값을 씁니다.|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
