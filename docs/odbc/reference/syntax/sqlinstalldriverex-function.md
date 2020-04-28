---
title: SQLInstallDriverEx 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverEx
helpviewer_keywords:
- SQLInstallDriverEx function [ODBC]
ms.assetid: 1dd74544-f4e9-46e1-9b5f-c11d84fdab4c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 054e8b6b9eae26bd5f973f3d46d7ef37363a8e79
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302125"
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 함수
**규칙**  
 소개 된 버전: ODBC 3.0  
  
 **요약**  
 **Sqlinstalldriverex** 는 시스템 정보의 odbcinst.ini 항목에 드라이버에 대 한 정보를 추가 하 고 드라이버의 *usagecount* 를 1 씩 증가 시킵니다. 그러나 드라이버의 버전이 이미 있지만 드라이버에 대 한 *Usagecount* 값이 없는 경우 새 *usagecount* 값은 2로 설정 됩니다.  
  
 이 함수는 실제로 파일을 복사 하지 않습니다. 드라이버의 파일을 대상 디렉터리에 올바르게 복사 하는 것은 호출 프로그램의 책임입니다.  
  
 ODBCCONF를 사용 하 여 **Sqlinstalldriverex** 의 기능에 액세스할 수도 있습니다 [. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLInstallDriverEx(  
     LPCSTR    lpszDriver,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDriver*  
 입력 실제 드라이버 이름 대신 사용자에 게 제공 되는 드라이버 설명 (일반적으로 연결 된 DBMS의 이름)입니다. *LpszDriver* 인수는 드라이버를 설명 하는 키워드-값 쌍의 이중 null 종료 목록을 포함 해야 합니다. 키워드-값 쌍에 대 한 자세한 내용은 [드라이버 사양 하위 키](../../../odbc/reference/install/driver-specification-subkeys.md)를 참조 하세요. 이중 null로 끝나는 문자열에 대 한 자세한 내용은 [ConfigDSN 함수](../../../odbc/reference/syntax/configdsn-function.md)를 참조 하세요.  
  
 *lpszPathIn*  
 입력 설치 대상 디렉터리의 전체 경로 이거나 null 포인터입니다. *LpszPathIn* 가 null 포인터인 경우 드라이버는 시스템 디렉터리에 설치 됩니다.  
  
 *lpszPathOut*  
 출력 드라이버를 설치 해야 하는 대상 디렉터리의 경로입니다. 드라이버를 이전에 설치 하지 않은 경우 *lpszPathOut* 은 *lpszPathIn*와 동일 해야 합니다. 드라이버가 이전에 설치 된 경우 *lpszPathOut* 은 이전 설치의 경로입니다.  
  
 *cbPathOutMax*  
 입력 *LpszPathOut*의 길이입니다.  
  
 *pcbPathOut*  
 출력 *LpszPathOut*에서 반환 하는 데 사용할 수 있는 null 종료 문자를 제외한 총 바이트 수입니다. 반환할 수 있는 바이트 수가 *Cbpathoutmax*보다 크거나 같으면 *lpszPathOut* 의 출력 경로가 *cbpathoutmax* 에서 null 종료 문자를 뺀 값으로 잘립니다. *Pcbpathout* 인수는 null 포인터 일 수 있습니다.  
  
 *fRequest*  
 입력 요청 유형입니다. *Frequest* 인수는 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_INSTALL_INQUIRY: 드라이버를 설치할 수 있는 위치를 조회 합니다.  
  
 ODBC_INSTALL_COMPLETE: 설치 요청을 완료 합니다.  
  
 *lpdwUsageCount*  
 출력 이 함수가 호출 된 후의 드라이버 사용 횟수입니다.  
  
 응용 프로그램은 사용 횟수를 설정 하면 안 됩니다. ODBC는이 수를 유지 합니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlinstalldriverex** 가 FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*LpszPathOut* 인수가 출력 경로를 포함할 만큼 크지 않습니다. 버퍼는 잘린 경로를 포함 합니다.<br /><br /> *Cbpathoutmax* 인수가 0이 고 *frequest* 가 ODBC_INSTALL_COMPLETE 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못 된 요청 유형|*Frequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|*LpszDriver* 인수에 구문 오류가 포함 되어 있습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못 된 설치 경로|*LpszPathIn* 인수에 잘못 된 경로가 포함 되어 있습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 번역기 설치 라이브러리를 로드할 수 없습니다.|드라이버 설치 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|잘못 된 매개 변수 시퀀스|*LpszDriver* 인수에 키워드-값 쌍의 목록이 없습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|구성 요소 사용 횟수를 증가 시키거나 감소 시킬 수 없습니다.|드라이버의 사용 횟수를 증분 하지 못했습니다.|  
  
## <a name="comments"></a>주석  
 *LpszDriver* 인수는 키워드-값 쌍 형식의 특성 목록입니다. 각 쌍은 null 바이트로 종료 되며 전체 목록이 null 바이트로 종료 됩니다. 즉, 두 개의 null 바이트가 목록의 끝을 표시 합니다. 이 목록의 형식은 다음과 같습니다.  
  
 _드라이버-desc_ **\\**0driver**=**_driver-dll-filename_**\\**0 [설치**=**_프로그램-dll-파일 이름_<b>\\</b>0]  
  
 [_driver-keyword1_**=**_value1_<b>\\</b>0] [_driver-attr-keyword2_**=**_value2_<b>\\</b>0] ... <b>\\</b>0  
  
 여기서 \ 0은 null 바이트이 고 *driver-keywordn* 은 any driver attribute 키워드입니다. 키워드는 지정 된 순서 대로 표시 되어야 합니다. 예를 들어 포맷 된 텍스트 파일용 드라이버에 별도의 드라이버와 설치 Dll이 있고 .txt 및 .csv 확장명을 가진 파일을 사용할 수 있다고 가정 합니다. 이 드라이버에 대 한 *lpszDriver* 인수는 다음과 같을 수 있습니다.  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 SQL Server 용 드라이버에 별도의 설치 DLL이 없고 드라이버 특성 키워드가 없는 것으로 가정 합니다. 이 드라이버에 대 한 *lpszDriver* 인수는 다음과 같을 수 있습니다.  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 **Sqlinstalldriverex** 가 *lpszDriver* 인수에서 드라이버에 대 한 정보를 검색 한 후 시스템 정보에 있는 ODBCINST.INI 항목의 [ODBC Drivers] 섹션에 드라이버 설명을 추가 합니다. 그런 다음 드라이버의 설명으로 섹션을 만들고 드라이버 DLL 및 설치 DLL의 전체 경로를 추가 합니다. 마지막으로 설치 된 대상 디렉터리의 경로를 반환 하지만 드라이버 파일을 복사 하지 않습니다. 호출 프로그램은 실제로 드라이버 파일을 대상 디렉터리에 복사 해야 합니다.  
  
 **Sqlinstalldriverex** 는 설치 된 드라이버에 대 한 구성 요소 사용 횟수를 1 씩 증가 시킵니다. 드라이버의 버전이 이미 있지만 드라이버의 구성 요소 사용 횟수가 없는 경우 새 구성 요소 사용 횟수 값은 2로 설정 됩니다.  
  
 응용 프로그램 설치 프로그램은 드라이버 파일을 물리적으로 복사 하 고 파일 사용 횟수를 유지 관리 하는 일을 담당 합니다. 드라이버 파일이 이전에 설치 되지 않은 경우 응용 프로그램 설치 프로그램은 *lpszPathIn* 경로에 파일을 복사 하 고 파일 사용 횟수를 만들어야 합니다. 파일이 이전에 설치 된 경우 설치 프로그램은 단순히 파일 사용 횟수를 늘리고 *lpszPathOut* 인수에서 이전 설치의 경로를 반환 합니다.  
  
> [!NOTE]  
>  구성 요소 사용 횟수 및 파일 사용 횟수에 대 한 자세한 내용은 [사용량 계산](../../../odbc/reference/install/usage-counting.md)을 참조 하세요.  
  
 이전 버전의 드라이버 파일이 응용 프로그램에서 이전에 설치 된 경우 드라이버를 제거한 후 다시 설치 하 여 드라이버 구성 요소 사용 횟수가 올바른지를 다시 설치 해야 합니다. **SQLConfigDriver** (ODBC_REMOVE_DRIVER의 *frequest* )를 먼저 호출한 다음 **SQLRemoveDriver** 를 호출 하 여 구성 요소 사용 횟수를 감소 시켜야 합니다. 그런 다음 **Sqlinstalldriverex** 를 호출 하 여 드라이버를 다시 설치 하 고 구성 요소 사용 횟수를 증가 시킵니다. 응용 프로그램 설치 프로그램에서 이전 파일을 새 파일로 바꾸어야 합니다. 파일 사용 횟수는 동일 하 게 유지 되 고 이전 버전 파일을 사용한 다른 모든 응용 프로그램은 이제 최신 버전을 사용 합니다.  
  
> [!NOTE]  
>  드라이버가 이전에 설치 되었고 **Sqlinstalldriverex** 를 호출 하 여 다른 디렉터리에 드라이버를 설치 하는 경우이 함수는 TRUE를 반환 하지만 *lpszPathOut* 는 드라이버가 이미 설치 된 디렉터리를 포함 합니다. *LpszDriver* 인수에 입력 한 디렉터리는 포함 되지 않습니다.  
  
 **Sqlinstalldriverex** 에서 *lpszPathOut* 의 경로 길이는 2 단계 설치 프로세스를 허용 하므로 응용 프로그램은 ODBC_INSTALL_INQUIRY 모드의 *Frequest* 를 사용 하 여 **Sqlinstalldriverex** 를 호출 하 여 어떤 *cbpathoutmax* 를 확인할 수 있습니다. 그러면 *Pcbpathout* 버퍼에서 사용할 수 있는 총 바이트 수가 반환 됩니다. 그런 다음 **Sqlinstalldriverex** 는 ODBC_INSTALL_COMPLETE의 *Frequest* 와 *pcbpathout* 버퍼의 값으로 설정 된 *cbpathoutmax* 인수 및 null 종료 문자를 사용 하 여 호출할 수 있습니다.  
  
 **Sqlinstalldriverex**에 대해 2 단계 모델을 사용 하지 않도록 선택 하는 경우 stdlib.h에 정의 된 대로 대상 디렉터리의 경로에 대 한 저장소 크기 _MAX_PATH를 정의 하는 *Cbpathoutmax*를 사용 하 여 잘림 방지를 설정 해야 합니다.  
  
 *Frequest* 가 ODBC_INSTALL_COMPLETE 되 면 **Sqlinstalldriverex** 에서 *LpszPathOut* 가 NULL (또는 *cbpathoutmax* 가 0 일 수 있음) 일 수 없습니다. *Frequest* 가 ODBC_INSTALL_COMPLETE 인 경우 반환할 수 있는 바이트 수가 *Cbpathoutmax*보다 크거나 같은 경우에는 잘림이 발생 하므로 FALSE가 반환 됩니다.  
  
 **Sqlinstalldriverex** 를 호출 하 고 응용 프로그램 설치 프로그램에서 드라이버 파일 (필요한 경우)을 복사한 후 드라이버 설치 DLL이 **SQLConfigDriver** 를 호출 하 여 드라이버의 구성을 설정 해야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|드라이버 관리자 설치|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
