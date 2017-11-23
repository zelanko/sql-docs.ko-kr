---
title: "SQLConfigDataSource 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLConfigDataSource
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLConfigDataSource
helpviewer_keywords: SQLConfigDataSource function [ODBC]
ms.assetid: f8d6e342-c010-434e-b1cd-f5371fb50a14
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e98f86c95e79effc45afdbc800f8e4eefaac3cd4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource 함수(SQLConfigDataSource Function)
**규칙**  
 ODBC 1.0 도입 된 버전:  
  
 **요약**  
 **SQLConfigDataSource** 추가, 수정 하거나 데이터 소스를 삭제 합니다.  
  
 기능 **SQLConfigDataSource** 로 액세스할 수도 [ODBCCONF 합니다. EXE](../../../odbc/odbcconf-exe.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLConfigDataSource(  
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
  
 ODBC_ADD_DSN: 새 사용자 데이터 원본을 추가 합니다.  
  
 ODBC_CONFIG_DSN: 구성 (수정) 기존 사용자 데이터 원본입니다.  
  
 하려면 ODBC_REMOVE_DSN: 기존 사용자 데이터 원본을 제거 합니다.  
  
 ODBC_ADD_SYS_DSN: 새 시스템 데이터 원본을 추가 합니다.  
  
 ODBC_CONFIG_SYS_DSN: 기존 시스템 데이터 원본을 수정 합니다.  
  
 ODBC_REMOVE_SYS_DSN: 기존 시스템 데이터 원본을 제거 합니다.  
  
 ODBC_REMOVE_DEFAULT_DSN: 시스템 정보에서 기본 데이터 원본 사양 섹션을 제거 합니다. (또한 기본 드라이버 사양 섹션에서에서 제거 시스템 정보에 Odbcinst.ini 항목입니다. 이 *문제점과* 사용 되지 않는와 동일한 기능을 수행 **SQLRemoveDefaultDataSource** 함수입니다.) 이 옵션을 지정 하는 경우에 대 한 호출에서 다른 매개 변수를 모두 **SQLConfigDataSource** 무시 됩니다 NULL 그러지 않은 경우; Null 이어야 합니다.  
  
 *lpszDriver*  
 [입력] 드라이버 설명 (일반적으로 연결된 되는 DBMS의 이름) 실제 드라이버 이름 대신 사용자에 게 표시 합니다.  
  
 *lpszAttributes*  
 [입력] 키워드-값 쌍의 형식에 특성 목록이 이중 null로 종료 합니다. 자세한 내용은 참조 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)합니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다. 시스템 정보에 없는 항목이 있으면이 함수를 호출할 때 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLConfigDataSource** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_INVALID_HWND|잘못 된 창 핸들|*창은* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|*문제점과* 인수는 다음 중 하나 였습니다.<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN 하려면 ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|잘못 된 드라이버 또는 변환기 이름입니다.|*lpszDriver* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|*lpszAttributes* 인수에 구문 오류가 포함 되어 있습니다.|  
|ODBC_ERROR_REQUEST_FAILED|*요청* 실패|설치 관리자가 요청한 작업을 수행할 수 없습니다는 *문제점과* 인수입니다. 에 대 한 호출 **ConfigDSN** 실패 했습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 변환기 설치 라이브러리를 로드할 수 없습니다.|드라이버 설치 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>설명  
 **SQLConfigDataSource** 의 값을 사용 하 여 *lpszDriver* 시스템 정보에서 드라이버 설치 DLL의 전체 경로 읽을 수 있습니다. DLL 및 호출 로드 **ConfigDSN** 를 통해 전달 된 동일한 인수를 사용 합니다.  
  
 **SQLConfigDataSource** 를 찾거나 설치 DLL을 로드할 수 없는 경우 하거나 대화 상자를 취소 하는 경우에 FALSE를 반환 합니다. 그렇지 않으면에서 받은 상태를 반환 **ConfigDSN**합니다.  
  
 **SQLConfigDataSource** 시스템 DSN 매핑합니다 *문제점과*사용자 DSN에 s *문제점과*(ODBC_ADD_SYS_DSN를 ODBC_ADD_DSN, ODBC_CONFIG_DSN, 및 ODBC_REMOVE_SYS ODBC_CONFIG_SYS_DSN s _DSN 하려면 ODBC_REMOVE_DSN에)입니다. 사용자 및 시스템 Dsn을 구분 하기 위해 **SQLConfigDataSource** 설치 관리자는 다음 표에 따라 구성 모드를 설정 합니다. 를 반환 하기 전에 **SQLConfigDataSource** 구성 모드 BOTHDSN을 기본값으로 다시 설정 합니다. **ConfigDSN** (드라이버에서 구현)를 호출 해야 **SQLWriteDSNToIni** 및 **SQLWritePrivateProfileString** 시스템 DSN을 지원 하도록 합니다. 자세한 내용은 참조 [ConfigDSN 함수](../../../odbc/reference/syntax/configdsn-function.md)합니다.  
  
|*문제점과*|구성 모드|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|하려면 ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 데이터 원본 제거|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (에 DLL 설치)|  
|시스템 정보에서 제거 하는 데이터 원본 이름|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|시스템 정보에는 데이터 원본 이름 추가|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
