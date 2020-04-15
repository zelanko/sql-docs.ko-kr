---
title: SQLRemove드라이버관리자 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriverManager
helpviewer_keywords:
- SQLRemoveDriverManager function function [ODBC]
ms.assetid: 3a41511f-6603-4b81-a815-7883874023c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 27b32c1c4e0f3f4d5359af287ba07d40b033af00
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301814"
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 함수
**규칙**  
 버전 소개: ODBC 3.0: Windows XP 서비스 팩 2, Windows 서버 2003 서비스 팩 1 및 이후 운영 체제에서 사용되지 않습니다.  
  
 **요약**  
 **SQLRemoveDriverManager** 변경 하거나 시스템 정보의 Odbcinst.ini 항목에서 ODBC 핵심 구성 요소에 대 한 정보를 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *pdw사용카운트*  
 [출력] 이 함수가 호출된 후 드라이버 관리자의 사용 횟수입니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다. 이 함수를 호출할 때 시스템 정보에 항목이 없으면 함수는 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLRemoveDriverManager** FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 관련 된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|레지스트리에서 구성 요소를 찾을 수 없습니다.|설치 관리자는 레지스트리에 없거나 레지스트리에서 찾을 수 없기 때문에 드라이버 관리자 정보를 제거할 수 없습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|구성 요소 사용량 수를 증가하거나 감소시킬 수 없습니다.|설치 프로그램이 드라이버 관리자의 사용 횟수를 감소시키지 못했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLRemoveDriverManager는** **SQLInstallDriverManager** 기능을 보완하고 시스템 정보의 구성 요소 사용 수를 업데이트합니다. 이 함수는 설치 응용 프로그램에서만 호출해야 합니다.  
  
 **SQLRemoveDriverManager는** 핵심 구성 요소 사용 수를 1로 줄입니다. 구성 요소 사용 수가 0으로 이동하면 입력 시스템 정보가 제거됩니다. 핵심 구성 요소 항목은 "ODBC 코어"라는 제목 아래 시스템 정보의 다음 위치에 있습니다.  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  구성 요소 사용량 이 수와 파일 사용 수가 0에 도달하면 응용 프로그램이 Driver Manager 파일을 물리적으로 제거해서는 안 됩니다.  
  
 **SQLRemoveDriverManager** 실제로 어떤 파일을 제거 하지 않습니다. 호출 프로그램은 파일을 삭제하고 파일 사용 수를 유지 관리합니다. 그러나 이러한 파일은 파일 사용 수를 증가시키지 않은 다른 응용 프로그램에서 사용할 수 있으므로 구성 요소 사용 수와 파일 사용 수가 모두 0에 도달하면 드라이버 관리자 파일을 제거해서는 안 됩니다.  
  
 **SQLRemoveDriverManager는** 제거 프로세스의 일부로 호출됩니다. ODBC 핵심 구성 요소(드라이버 관리자, 커서 라이브러리, 설치 관리자, 언어 라이브러리, 관리자, 파일 을 던지며 포함)는 전체적으로 제거됩니다. **SQLRemoveDriverManager제거** 프로세스의 일부로 호출 될 때 다음 파일이 제거 되지 않습니다.  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32. Dll|  
|ODBCCR32. Dll|ODBC16GT. Dll|  
|ODBCCU32. Dll|ODBC32GT. Dll|  
|ODBCINT. Dll|DS16GT. Dll|  
|ODBCTRAC. Dll|DS32GT. Dll|  
|MSVCRT40. Dll|ODBCAD32. Exe|  
|ODBCCP32. Cpl||  
  
 **SQLRemoveDriverManager는** 업그레이드 프로세스의 일부로 호출됩니다. 응용 프로그램이 업그레이드를 수행해야 하고 이전에 드라이버를 설치한 것을 감지한 경우 드라이버를 제거한 다음 다시 설치해야 합니다.  
  
 **SQLRemoveDriverManager** 먼저 구성 요소 사용 수를 감소 시키기 위해 호출 해야 합니다. 그런 다음 **SQLInstallDriverEx를** 호출하여 구성 요소 사용량 수를 증가시켜야 합니다. 응용 프로그램 설치 프로그램은 이전 핵심 구성 요소 파일을 새 파일로 바꿔야 합니다. 파일 사용 수는 동일하게 유지되며 이전 버전 핵심 구성 요소 파일을 사용하는 다른 응용 프로그램은 이제 최신 버전 파일을 사용합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|드라이버 관리자 설치|[SQLInstallDriver관리자](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
