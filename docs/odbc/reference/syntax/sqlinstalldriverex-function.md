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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5664a4cb745a250aa8db6d98b92a275bb91c7a8d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536576"
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 함수
**규칙**  
 도입 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLInstallDriverEx** Odbcinst.ini 항목 시스템 정보를 드라이버에 대 한 정보를 추가 하 고 드라이버를 증가 시킵니다 *UsageCount* 1만 합니다. 그러나는 버전의 드라이버를 이미 있지만 *UsageCount* 존재 하지 않는 드라이버에 대 한 값 새 *UsageCount* 값이 2로 설정 합니다.  
  
 이 함수는 모든 파일을 실제로 복사 하지 않습니다. 대상 디렉터리에 드라이버 파일을 제대로 복사할 호출 프로그램의 담당 합니다.  
  
 기능의 **SQLInstallDriverEx** 사용 하 여 액세스할 수도 있습니다 [ODBCCONF 합니다. EXE](../../../odbc/odbcconf-exe.md)합니다.  
  
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
 [입력] 실제 드라이버 이름 대신 사용자에 게 표시 드라이버 설명 (일반적으로 연결된 되는 DBMS의 이름)입니다. 합니다 *lpszDriver* 인수 드라이버를 설명 하는 키워드 / 값 쌍을 이중으로 null로 끝나는 목록에 포함 되어야 합니다. 키워드-값 쌍에 대 한 자세한 내용은 참조 하세요. [드라이버 사양 하위 키](../../../odbc/reference/install/driver-specification-subkeys.md)합니다. 이중으로 null로 끝나는 문자열에 대 한 자세한 내용은 참조 하세요. [ConfigDSN 함수](../../../odbc/reference/syntax/configdsn-function.md)합니다.  
  
 *lpszPathIn*  
 [입력] 설치 또는 null 포인터의 대상 디렉터리의 전체 경로입니다. 하는 경우 *lpszPathIn* 가 null 포인터인 경우 드라이버 시스템 디렉터리에 설치 됩니다.  
  
 *lpszPathOut*  
 [출력] 드라이버를 설치할 대상 디렉터리의 경로입니다. 드라이버 이전에 설치 되지 않은 경우 *lpszPathOut* 와 동일 해야 *lpszPathIn*합니다. 드라이버 이전에 설치한 경우 *lpszPathOut* 이전 설치의 경로입니다.  
  
 *cbPathOutMax*  
 [입력] 길이가 *lpszPathOut*합니다.  
  
 *pcbPathOut*  
 [출력] 총 바이트 (null 종결 문자가 제외)에서 반환할 사용 가능한 *lpszPathOut*합니다. 반환할 사용 가능한 바이트 수가 보다 크거나 같은 경우 *cbPathOutMax*, 출력 경로 *lpszPathOut* 잘립니다 *cbPathOutMax* 빼기는 null 종료 문자입니다. 합니다 *pcbPathOut* 인수로 null 포인터를 사용할 수 있습니다.  
  
 *fRequest*  
 [입력] 요청 유형입니다. 합니다 *문제점과* 인수는 다음 값 중 하나를 포함 해야 합니다.  
  
 ODBC_INSTALL_INQUIRY: 드라이버를 설치할 수 있는지 문의 합니다.  
  
 ODBC_INSTALL_COMPLETE: 설치 요청을 완료 합니다.  
  
 *lpdwUsageCount*  
 [출력] 이 함수를 호출한 후 드라이버의 사용 횟수입니다.  
  
 응용 프로그램 사용 횟수를 설정 하지 않아야 합니다. ODBC는이 개수를 유지 합니다.  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLInstallDriverEx** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|합니다 *lpszPathOut* 인수가 출력 경로 포함 하기에 충분 합니다. 버퍼의 잘린된 경로 포함합니다.<br /><br /> 합니다 *cbPathOutMax* 인수가 0, 및 *문제점과* ODBC_INSTALL_COMPLETE 되었습니다.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|요청의 형식이 잘못 되었습니다|합니다 *문제점과* 인수 중 하나 였습니다.<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못 된 키워드-값 쌍|합니다 *lpszDriver* 인수 구문 오류를 포함 합니다.|  
|ODBC_ERROR_INVALID_PATH|잘못 된 설치 경로|합니다 *lpszPathIn* 인수에 잘못 된 경로 포함 합니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 translator 설치 라이브러리를 로드할 수 없습니다.|드라이버 설치 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|잘못 된 매개 변수 순서|합니다 *lpszDriver* 인수 키워드-값 쌍의 목록이 없습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|증가 또는 구성 요소 사용 횟수를 감소 시킬 수 없습니다.|설치 관리자는 드라이버의 사용 횟수를 증가 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 합니다 *lpszDriver* 인수는 키워드 / 값 쌍의 형태로 특성 목록입니다. 각 쌍을 null 바이트를 사용 하 여 종료 됩니다 하 고 전체 목록을 null 바이트를 사용 하 여 종료 됩니다. (즉, 두 개의 null 바이트의 끝을 표시 목록입니다.) 이 목록의 형식은 아래와 같습니다.  
  
 _driver-desc_ **\\** 0Driver **=** _driver-DLL-filename_ **\\** 0[Setup **=** _setup-DLL-filename_<b>\\</b>0]  
  
 [_driver-attr-keyword1_ **=** _value1_<b>\\</b>0][_driver-attr-keyword2_ **=** _value2_<b>\\</b>0]...<b>\\</b>0  
  
 \0 null 바이트를 인지 하는 위치 및 *드라이버-attr-keywordn* 모든 드라이버 특성 키워드입니다. 키워드는 지정된 된 순서 대로 나타나야 합니다. 예를 들어, 가정 서식 있는 텍스트 파일에 대 한 드라이버를 별도 드라이버 설치 Dll 및.csv 및.txt 확장명을 가진 파일을 사용할 수 있습니다. 합니다 *lpszDriver* 이 드라이버에 대 한 인수는 다음과 같을 수 있습니다.  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 SQL Server에 대 한 드라이버 DLL을 별도 설치 되지 않은 드라이버 특성 키워드 없는 만든다고 가정 합니다. 합니다 *lpszDriver* 이 드라이버에 대 한 인수는 다음과 같을 수 있습니다.  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 한 후 **SQLInstallDriverEx** 에서 드라이버에 대 한 정보를 검색 합니다 *lpszDriver* 인수를 시스템에서 드라이버 파일에 대 한 설명을 Odbcinst.ini 항목의 [ODBC Drivers] 섹션에 추가 정보입니다. 그런 다음 드라이버의 설명 섹션을 만들고 드라이버 DLL의 전체 경로 및 설치 DLL 추가 합니다. 마지막으로 설치의 대상 디렉터리의 경로 반환 하지만 드라이버 파일을 복사 하지 않습니다. 실제로 호출 프로그램 대상 디렉터리에 드라이버 파일을 복사 해야 합니다.  
  
 **SQLInstallDriverEx** 설치 된 드라이버에 대 한 구성 요소 사용 횟수를 1 씩 증가 합니다. 드라이버의 버전을 이미 있지만 드라이버에 대 한 구성 요소 사용 수 없는 경우, 새 구성 요소 사용 개수 값을 2로 설정 됩니다.  
  
 응용 프로그램 설치 프로그램은 드라이버 파일을 복사 하는 물리적으로 및 파일 사용 횟수를 유지 관리 하는 일을 담당 합니다. 드라이버 파일을 이전에 설치 되지 않은 경우 응용 프로그램 설치 프로그램에서 파일을 복사 해야 합니다 *lpszPathIn* 경로 파일 사용 횟수를 만듭니다. 파일을 이전에 설치한 경우 설치 프로그램을 단순히 파일 사용 횟수를 증가 하 고 이전 설치의 경로 반환 합니다 *lpszPathOut* 인수입니다.  
  
> [!NOTE]  
>  구성 요소 사용 횟수 및 파일 사용 횟수에 대 한 자세한 내용은 참조 하세요. [사용량 계산](../../../odbc/reference/install/usage-counting.md)합니다.  
  
 드라이버 파일의 이전 버전을 응용 프로그램에서 설치 했던 것 경우 드라이버를 제거 하 고 다시 설치 드라이버 구성 요소 사용 횟수는 유효한 해야 합니다. **SQLConfigDriver** (사용 하 여는 *문제점과* ODBC_REMOVE_DRIVER의) 먼저를 호출 해야 차례로 **SQLRemoveDriver** 구성 요소 사용 횟수를 감소 시키기 위해 호출 해야 합니다. **SQLInstallDriverEx** 구성 요소 사용 횟수를 증분 하 여 드라이버를 다시 설치 하려면 다음 호출 해야 합니다. 응용 프로그램 설치 프로그램을 새 파일로 이전 파일을 바꾸어야 합니다. 파일 사용 횟수를 동일 하 게 유지 됩니다 및 이전 버전 파일을 사용 하는 다른 응용 프로그램에서 이제 최신 버전을 사용 합니다.  
  
> [!NOTE]  
>  드라이버에서 이전에 설치 된 경우 및 **SQLInstallDriverEx** 함수는 TRUE를 반환 다른 디렉터리에 드라이버를 설치 하기 위해 호출 하지만 *lpszPathOut* 디렉터리에 포함될지 여기서 드라이버 이미 설치 되었습니다. 입력 한 디렉터리를 포함 하지 것입니다 합니다 *lpszDriver* 인수입니다.  
  
 경로의 길이 *lpszPathOut* 에 **SQLInstallDriverEx** 응용 프로그램 항목을 확인할 수 있도록 2 단계 설치 프로세스에 대 한 허용 *cbPathOutMax* 여야 합니다 호출 **SQLInstallDriverEx** 사용 하 여는 *문제점과* ODBC_INSTALL_INQUIRY 모드입니다. 사용 가능한 바이트의 총 수를 반환은이 *pcbPathOut* 버퍼입니다. **SQLInstallDriverEx** 사용 하 여 호출할 수 있습니다는 *문제점과* ODBC_INSTALL_COMPLETE의 및 *cbPathOutMax* 인수를 값으로 설정 된 *pcbPathOut*버퍼와 null 종료 문자입니다.  
  
 에 대 한 2 단계 모델을 사용 하도록 하지 않으려는 경우 **SQLInstallDriverEx**를 설정 해야 *cbPathOutMax*,으로 대상 디렉터리로 값 _max_path(256의 경로 대 한 저장소의 크기를 정의 하는 잘림을 방지 하기 위해 Stdlib.h에 정의 합니다.  
  
 때 *문제점과* ODBC_INSTALL_COMPLETE에는 **SQLInstallDriverEx** 없도록 *lpszPathOut* NULL로 (또는 *cbPathOutMax* 되도록 0)입니다. 하는 경우 *문제점과* ODBC_INSTALL_COMPLETE를 반환할 수 있는 바이트 수가 보다 크거나 같은 경우 FALSE 반환 됩니다 *cbPathOutMax*, 결과 사용 하 여 잘림이 발생 합니다.  
  
 이후에 **SQLInstallDriverEx** 호출한 (필요한 경우) 응용 프로그램 설치 프로그램에 드라이버 파일에 복사 하 고, 드라이버 설치 DLL을 호출 해야 합니다 **SQLConfigDriver** 에 대 한 구성을 설정 하는 드라이버입니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|드라이버 관리자 설치|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
