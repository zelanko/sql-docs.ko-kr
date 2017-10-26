---
title: "ConfigDSN 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 491396da26d75d6710e708b840c9407b4a976bb9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="configdsn-function"></a>ConfigDSN 함수
**규칙**  
 ODBC 1.0 도입 된 버전:  
  
 **요약**  
 **ConfigDSN** 추가, 수정 하거나, 시스템 정보에서 데이터 소스를 삭제 합니다. 이 옵션에 연결 정보에 대 한 사용자를 요청 수 있습니다. 드라이버 DLL 또는 별도 설치 DLL에서 가능 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL ConfigDSN(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>인수  
 *창은*  
 [입력] 부모 창 핸들입니다. 핸들 null 이면 함수는 모든 대화 상자 표시 되지 않습니다.  
  
 *문제점과*  
 [입력] 요청의 유형입니다. *문제점과* 인수는 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_ADD_DSN: 새 데이터 원본을 추가 합니다.  
  
 ODBC_CONFIG_DSN: 구성 (수정) 기존 데이터 원본입니다.  
  
 하려면 ODBC_REMOVE_DSN: 기존 데이터 원본을 제거 합니다.  
  
 *lpszDriver*  
 [입력] 드라이버 설명 (일반적으로 연결된 되는 DBMS의 이름) 실제 드라이버 이름 대신 사용자에 게 표시 합니다.  
  
 *lpszAttributes*  
 [입력] 키워드-값 쌍의 형식에 특성 목록이 이중 null로 종료 합니다. 자세한 내용은 "설명"을 참조 하십시오.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **ConfigDSN** 관련 FALSE를 반환 * \*pfErrorCode* 를 호출 하 여 설치 관리자 오류 버퍼에 값이 게시 **SQLPostInstallerError** 및 호출 하 여 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에 * \*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|잘못 된 창 핸들|*창은* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|*lpszAttributes* 인수에 구문 오류가 포함 되어 있습니다.|  
|ODBC_ERROR_INVALID_NAME|잘못 된 드라이버 또는 변환기 이름입니다.|*lpszDriver* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|*문제점과* 인수는 다음 중 하나 였습니다.<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN 하려면 ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|요청한 작업을 수행할 수 없습니다는 *문제점과* 인수입니다.|  
|ODBC_ERROR_DRIVER_SPECIFIC|드라이버 또는 변환기 관련 오류|정의 된 ODBC 설치 관리자 오류가 없는 드라이버 관련 오류가 발생 했습니다. *SzError* 에 대 한 호출의 인수는 **SQLPostInstallerError** 함수에는 드라이버 특정 오류 메시지가 포함 되어 있어야 합니다.|  
  
## <a name="comments"></a>설명  
 **ConfigDSN** 키워드-값 쌍의 형식에 특성의 목록으로 DLL 설치 관리자에서 연결 정보를 받습니다. 각 쌍은 null 바이트를으로 종료 되 고 전체 목록을 바이트 null로 종료 됩니다. (즉, 두 개의 null 바이트의 끝을 표시 목록입니다.) 키워드 / 값 쌍의 등호 엔 공백이 허용 되지 않습니다. **ConfigDSN** 키워드에 대 한 유효한 키워드를 수락할 수 있는 **SQLBrowseConnect** 및 **SQLDriverConnect**합니다. **ConfigDSN** 에서는 반드시 지원에 대 한 유효한 키워드는 모든 키워드 **SQLBrowseConnect** 및 **SQLDriverConnect**합니다. (**ConfigDSN** 을 허용 하지 않습니다는 **드라이버** 키워드입니다.) 사용 하는 키워드는 **ConfigDSN** 함수는 다시 설치 프로그램의 자동 설정 기능을 사용 하 여 데이터 소스를 만드는 데 필요한 모든 옵션을 지원 해야 합니다. 때의 용도 **ConfigDSN** 값과 연결 문자열 값은 동일한, 동일한 키워드를 사용 해야 합니다.  
  
 와 같이 **SQLBrowseConnect** 및 **SQLDriverConnect**, 키워드 및 해당 값 포함 되 면 안는 **{} (),? \*=! @** 문자와의 값은 **DSN** 키워드 공백으로 구성 될 수 없습니다. 키워드 및 데이터 원본 이름 레지스트리 문법 때문에 백슬래시를 포함할 수 없습니다 (\\) 문자.  
  
 **ConfigDSN** 호출 해야 **SQLValidDSN** 데이터 원본 이름의 길이 확인 하 고 이름에 잘못 된 문자가 포함 되어 있는지 확인 합니다. 데이터 원본 이름 SQL_MAX_DSN_LENGTH 보다 길면 또는 잘못 된 문자를 포함 하는 경우 **SQLValidDSN** 에서 오류를 반환 하 고 **ConfigDSN** 에서 오류를 반환 합니다. 데이터 원본 이름의 길이 확인란도 선택 하 여 **SQLWriteDSNToIni**합니다.  
  
 예를 들어 사용자 ID, 암호 및 데이터베이스 이름을 요구 하는 데이터 원본을 구성 하려면 설치 응용 프로그램에는 다음 키워드-값 쌍 전달 될 수 있습니다.  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 이러한 키워드에 대 한 자세한 내용은 참조 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 및 각 드라이버의 설명서입니다.  
  
 대화 상자를 표시 하려면 *창은* null이 아니어야 합니다.  
  
## <a name="adding-a-data-source"></a>데이터 원본 추가  
 데이터 원본 이름에 전달 되 면 **ConfigDSN** 에 *lpszAttributes*, **ConfigDSN** 이름이 유효한 지 확인 합니다. 데이터 원본 이름은 기존 데이터 원본 이름과 일치 하는 경우 및 *창은* 매개 변수가 null 이면 **ConfigDSN** 기존 이름을 덮어씁니다. 기존 이름을 일치 하는 경우 및 *창은* null이 아니면 **ConfigDSN** 덮어쓸 기존 이름을 하 라는 메시지를 표시 합니다.  
  
 경우 *lpszAttributes* 데이터 원본에 연결 하는 데 충분 한 정보가 포함 **ConfigDSN** 데이터 원본 또는 사용자는 연결 정보를 변경할 수 있는 대화 상자에 추가할 수 있습니다. 경우 *lpszAttributes* 데이터 원본에 연결 하는 데 충분 한 정보는 **ConfigDSN** 경우; 필요한 정보를 결정 해야 *창은* 은 null로, 사용자 로부터 정보를 검색 하는 대화 상자가 표시 됩니다.  
  
 경우 **ConfigDSN** 대화 상자를 표시에서 전달 된 모든 연결 정보를 표시 해야 *lpszAttributes*합니다. 특히, 데이터 원본 이름,에 전달 된 경우 **ConfigDSN** 해당 이름을 표시 하지만 변경할 사용자를 허용 하지 않습니다. **ConfigDSN** 전달 되지 않으므로 연결 정보에 대 한 기본값을 제공할 수 *lpszAttributes*합니다.  
  
 경우 **ConfigDSN** 전체 연결 정보를 가져올 수 없는 데이터 원본에 대해 FALSE를 반환 합니다.  
  
 경우 **ConfigDSN** 데이터 원본에 대 한 완전 한 연결 정보를 얻을 수, 호출 **SQLWriteDSNToIni** Odbc.ini 파일 (또는 레지스트리)에 새 데이터 원본 지정을 추가 하려면 DLL이 설치 관리자에서 합니다. **SQLWriteDSNToIni** 데이터 원본 이름 [ODBC 데이터 소스] 섹션에 추가 데이터 원본 사양 섹션, 만들고 추가 **드라이버** 키워드와 해당 값으로 드라이버 설명 합니다. **ConfigDSN** 호출 **SQLWritePrivateProfileString** 설치 관리자 추가 키워드 및 드라이버에 의해 사용 되는 값을 추가 하는 DLL에에서 있습니다.  
  
## <a name="modifying-a-data-source"></a>데이터 원본 수정  
 데이터 원본을 수정 하려면 데이터 원본 이름으로 전달 해야 **ConfigDSN** 에 *lpszAttributes*합니다. **ConfigDSN** Odbc.ini 파일 (또는 레지스트리)에서 데이터 원본 이름 인지 확인 합니다.  
  
 경우 *창은* 매개 변수가 null 이면 **ConfigDSN** 의 정보를 사용 하 여 *lpszAttributes* Odbc.ini 파일 (또는 레지스트리)에 대 한 정보를 수정할 수 있습니다. 경우 *창은* null이 아니면 **ConfigDSN** 의 정보를 사용 하 여 대화 상자를 표시 *lpszAttributes*에 없는 정보에 대 한; *lpszAttributes *, 시스템 정보에서 정보를 사용 합니다. 사용자가 수정할 수 전에 정보 **ConfigDSN** 시스템 정보에 저장 합니다.  
  
 데이터 원본 이름이 변경 된 경우 **ConfigDSN** 첫 번째로 호출 **SQLRemoveDSNFromIni** 설치 관리자에서 기존 데이터를 제거 하는 DLL 소스 Odbc.ini 파일 (또는 레지스트리에서) 사양입니다. 그런 다음 새 데이터 소스 사양을 추가 하려면 이전 섹션의 단계를 따릅니다. 데이터 원본 이름은 변경 되지 않았습니다 경우 **ConfigDSN** 호출 **SQLWritePrivateProfileString** 기타 변경을 수행 하려면 DLL이 설치 관리자에서 합니다. **ConfigDSN** 삭제 하거나 값을 변경할 수는 **드라이버** 키워드입니다.  
  
## <a name="deleting-a-data-source"></a>데이터 원본 삭제  
 데이터 소스를 삭제 하려면 데이터 원본 이름으로 전달 해야 **ConfigDSN** 에 *lpszAttributes*합니다. **ConfigDSN** Odbc.ini 파일 (또는 레지스트리)에서 데이터 원본 이름 인지 확인 합니다. 그런 다음 연속 호출 **SQLRemoveDSNFromIni** 데이터 원본을 제거 하려면 DLL이 설치 관리자에서 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 데이터 원본 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Odbc.ini 파일 또는 레지스트리 값을 가져올|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|기본 데이터 원본 제거|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Odbc.ini (또는 레지스트리)에서 제거 하는 데이터 원본 이름|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|데이터 원본 이름을 Odbc.ini (또는 레지스트리)에 추가|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Odbc.ini 파일 또는 레지스트리 값을 쓸|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|

