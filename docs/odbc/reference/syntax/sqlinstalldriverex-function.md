---
title: SQLInstallDriverEx 함수 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302125"
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 함수
**규칙**  
 버전 출시: ODBC 3.0  
  
 **요약**  
 **SQLInstallDriverEx는** 시스템 정보의 Odbcinst.ini 항목에 드라이버에 대한 정보를 추가하고 드라이버의 *사용 수를* 1씩 증가시입니다. 그러나 드라이버 버전이 이미 있지만 드라이버에 대한 *UsageCount* 값이 없는 경우 새 *UsageCount* 값은 2로 설정됩니다.  
  
 이 함수는 실제로 파일을 복사하지 않습니다. 드라이버의 파일을 대상 디렉터리로 올바르게 복사하는 것은 호출 프로그램의 책임입니다.  
  
 **SQLInstallDriverEx의** 기능은 ODBCCONF로도 액세스할 수 [있습니다. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 *lpsz드라이버*  
 [입력] 실제 드라이버 이름 대신 사용자에게 표시되는 드라이버 설명(일반적으로 연결된 DBMS의 이름)입니다. *lpszDriver* 인수에는 드라이버를 설명하는 키워드 값 쌍의 이중 null 종료 목록이 포함되어야 합니다. 키워드-값 쌍에 대한 자세한 내용은 [드라이버 사양 하위 키를](../../../odbc/reference/install/driver-specification-subkeys.md)참조하십시오. 이중 null 종료 문자열에 대한 자세한 내용은 [ConfigDSN 함수를](../../../odbc/reference/syntax/configdsn-function.md)참조하십시오.  
  
 *lpszPathIn*  
 [입력] 설치의 대상 디렉토리 또는 null 포인터의 전체 경로입니다. *lpszPathIn이* null 포인터인 경우 드라이버가 시스템 디렉토리에 설치됩니다.  
  
 *lpsz패스아웃*  
 [출력] 드라이버를 설치해야 하는 대상 디렉터리 경로입니다. 드라이버가 이전에 설치되지 않은 경우 *lpszPathOut은* *lpszPathIn*. 드라이버가 이전에 설치된 경우 *lpszPathOut은* 이전 설치의 경로입니다.  
  
 *cb패스아웃맥스*  
 [입력] *lpszPathOut의*길이 .  
  
 *pcb패스아웃*  
 [출력] *lpszPathOut에서*반환할 수 있는 총 바이트 수(null-종료 문자 제외). 반환할 수 있는 바이트 수가 *cbPathOutMax보다*크거나 같으면 *lpszPathOut의* 출력 경로가 *cbPathOutMax에서* null 종료 문자를 뺀 값으로 잘립니다. *pcbPathOut* 인수는 null 포인터일 수 있습니다.  
  
 *f요청*  
 [입력] 요청 유형입니다. *fRequest* 인수에는 다음 값 중 하나가 포함되어야 합니다.  
  
 ODBC_INSTALL_INQUIRY: 드라이버를 설치할 수 있는 위치에 대해 문의하십시오.  
  
 ODBC_INSTALL_COMPLETE: 설치 요청을 완료합니다.  
  
 *lpdw사용계산*  
 [출력] 이 함수가 호출된 후 드라이버의 사용 횟수입니다.  
  
 응용 프로그램은 사용 수를 설정해서는 안 됩니다. ODBC는 이 수를 유지합니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLInstallDriverEx가 FALSE를** 반환하는 경우 **SQLInstallerError**를 호출하여 연결된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못된 버퍼 길이|*lpszPathOut* 인수는 출력 경로를 포함할 만큼 충분히 크지 않았습니다. 버퍼에 잘린 경로가 포함되어 있습니다.<br /><br /> *cbPathOutMax* 인수는 0이고 *fRequest는* ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|잘못된 요청 유형|*fRequest* 인수는 다음 중 하나가 아닙니다.<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|잘못된 키워드-값 쌍|*lpszDriver* 인수에는 구문 오류가 포함되어 있습니다.|  
|ODBC_ERROR_INVALID_PATH|잘못된 설치 경로|*lpszPathIn* 인수에 잘못된 경로가 포함되어 있습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 번역기 설정 라이브러리를 로드할 수 없습니다.|드라이버 설정 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|잘못된 매개 변수 시퀀스|*lpszDriver* 인수에는 키워드 값 쌍 목록이 포함되어 있지 않았습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|구성 요소 사용량 수를 증가하거나 감소시킬 수 없습니다.|설치 프로그램이 드라이버의 사용 횟수를 증가시키지 못했습니다.|  
  
## <a name="comments"></a>주석  
 *lpszDriver* 인수는 키워드 값 쌍의 형태로 특성 의 목록입니다. 각 쌍은 null 바이트로 종료되고 전체 목록은 null 바이트로 종료됩니다. 즉, 두 개의 null 바이트가 목록의 끝을 표시합니다. 이 목록의 형식은 다음과 같습니다.  
  
 _드라이버-desc_ **\\****=** 0드라이버_드라이버-DLL 파일 이름_**\\****=** 0[설치_설정-DLL 파일 이름_<b>\\</b>0]  
  
 _[드라이버-attr-키워드1_**=**_value1_<b>\\</b>0] _[드라이버-attr-키워드2_**=**_value2_<b>\\</b>0]... <b>\\</b>0  
  
 여기서 \0은 null 바이트이고 *드라이버-attr-키워드는* 모든 드라이버 특성 키워드입니다. 키워드는 지정된 순서로 표시되어야 합니다. 예를 들어 서식이 지정된 텍스트 파일의 드라이버에 별도의 드라이버 및 설정 DLL이 있고 .txt 및 .csv 확장자와 함께 파일을 사용할 수 있다고 가정합니다. 이 드라이버에 대한 *lpszDriver* 인수는 다음과 같습니다.  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 SQL Server용 드라이버에 별도의 설정 DLL이 없고 드라이버 특성 키워드가 없다고 가정합니다. 이 드라이버에 대한 *lpszDriver* 인수는 다음과 같습니다.  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 **SQLInstallDriverEx는** *lpszDriver* 인수에서 드라이버에 대한 정보를 검색한 후 시스템 정보의 Odbcinst.ini 항목의 [ODBC 드라이버] 섹션에 드라이버 설명을 추가합니다. 그런 다음 드라이버 설명이 있는 섹션을 만들고 드라이버 DLL 및 설정 DLL의 전체 경로를 추가합니다. 마지막으로 설치의 대상 디렉터리 경로를 반환하지만 드라이버 파일을 복사하지는 않습니다. 호출 프로그램은 실제로 드라이버 파일을 대상 디렉터리로 복사해야 합니다.  
  
 **SQLInstallDriverEx는** 설치된 드라이버에 대한 구성 요소 사용 수를 1로 증가시입니다. 드라이버 버전이 이미 있지만 드라이버의 구성 요소 사용 수가 없는 경우 새 구성 요소 사용 개수 값이 2로 설정됩니다.  
  
 응용 프로그램 설치 프로그램은 드라이버 파일을 물리적으로 복사하고 파일 사용 수를 유지 관리합니다. 드라이버 파일이 이전에 설치되지 않은 경우 응용 프로그램 설치 프로그램은 *lpszPathIn* 경로에서 파일을 복사하고 파일 사용 수를 만들어야 합니다. 파일이 이전에 설치된 경우 설치 프로그램은 파일 사용 수를 증가시키고 *lpszPathOut* 인수에서 이전 설치 경로를 반환합니다.  
  
> [!NOTE]  
>  구성 요소 사용 수 및 파일 사용 수에 대한 자세한 내용은 [사용 계수를](../../../odbc/reference/install/usage-counting.md)참조하십시오.  
  
 응용 프로그램에서 이전 버전의 드라이버 파일을 설치한 경우 드라이버 구성 요소 사용 수가 유효하므로 드라이버를 제거한 다음 다시 설치해야 합니다. **SQLConfigDriver** *(ODBC_REMOVE_DRIVER fRequest)를* 먼저 호출해야하며 **SQLRemoveDriver는** 구성 요소 사용 수를 감소시키기 위해 호출해야합니다. 그런 다음 **SQLInstallDriverEx를** 호출하여 드라이버를 다시 설치하여 구성 요소 사용량을 증가시켜야 합니다. 응용 프로그램 설치 프로그램은 이전 파일을 새 파일로 바꿔야 합니다. 파일 사용 수는 동일하게 유지되며 이전 버전 파일을 사용한 다른 응용 프로그램은 이제 최신 버전을 사용합니다.  
  
> [!NOTE]  
>  드라이버가 이전에 설치되었고 **SQLInstallDriverEx가** 다른 디렉터리에서 드라이버를 설치하도록 호출된 경우 함수는 TRUE를 반환하지만 *lpszPathOut에는* 드라이버가 이미 설치된 디렉터리가 포함됩니다. *lpszDriver* 인수에 입력된 디렉터리에는 포함되지 않습니다.  
  
 **SQLInstallDriverEx에서** *lpszPathOut의* 경로 길이는 2단계 설치 프로세스를 허용하므로 응용 프로그램은 ODBC_INSTALL_INQUIRY 모드의 *fRequest를* 사용하여 **SQLInstallDriverEx를** 호출하여 *어떤 cbPathOutMax를* 호출해야 하는지 결정할 수 있습니다. 이렇게 하면 *pcbPathOut* 버퍼에서 사용할 수 있는 총 바이트 수가 반환됩니다. 그런 다음 **SQLInstallDriverEx는** ODBC_INSTALL_COMPLETE *fRequest와* *pcbPathOut* 버퍼의 값으로 설정된 *cbPathOutMax* 인수와 null 종료 문자로 호출할 수 있습니다.  
  
 **SQLInstallDriverEx에**대한 2단계 모델을 사용하지 않도록 선택한 경우 잘림을 방지하기 위해 대상 디렉터리 경로에 대한 저장소 크기를 stdlib.h에 정의된 값 _MAX_PATH *cbPathOutMax를*설정해야 합니다.  
  
 *fRequest가* ODBC_INSTALL_COMPLETE **경우 SQLInstallDriverEx는** *lpszPathOut을* NULL(또는 *cbPathOutMax가* 0)으로 허용하지 않습니다. *fRequest가* ODBC_INSTALL_COMPLETE 경우 반환할 수 있는 바이트 수가 *cbPathOutMax보다*크거나 같을 때 FALSE가 반환되고 그 결과 잘림이 발생합니다.  
  
 **SQLInstallDriverEx가** 호출되고 응용 프로그램 설치 프로그램이 드라이버 파일을 복사한 경우(필요한 경우) 드라이버 설치 DLL은 **SQLConfigDriver를** 호출하여 드라이버에 대한 구성을 설정해야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|드라이버 관리자 설치|[SQLInstallDriver관리자](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
