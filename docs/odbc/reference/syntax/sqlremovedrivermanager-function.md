---
title: SQLRemoveDriverManager 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5cd31a45ed891a8dc95f4f23981d4b626a6095b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024544"
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 함수
**규칙**  
 도입 된 버전: ODBC 3.0: Windows XP 서비스 팩 2, Windows Server 2003 서비스 팩 1 이상 운영 체제에서 사용 되지 않습니다.  
  
 **요약**  
 **SQLRemoveDriverManager** 변경 또는 시스템 정보 Odbcinst.ini 항목에서 ODBC 핵심 구성 요소에 대 한 정보를 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *pdwUsageCount*  
 [출력] 사용 횟수 드라이버 관리자의이 함수를 호출한 후입니다.  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다. 이 함수가 호출 될 때 시스템 정보에 없는 항목이 있으면 함수는 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLRemoveDriverManager** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|레지스트리에서 찾을 수 없습니다 하는 구성 요소|설치 관리자는 레지스트리에 없는 또는 레지스트리에서 찾을 수 없습니다 때문에 드라이버 관리자 정보를 제거 하지 못했습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|증가 또는 구성 요소 사용 횟수를 감소 시킬 수 없습니다.|드라이버 관리자의 사용 횟수를 감소 시키기 위해 설치 프로그램 실패 했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 **SQLRemoveDriverManager** 보완 합니다 **SQLInstallDriverManager** 함수 및 시스템 정보에는 구성 요소 사용을 계산 하는 업데이트 합니다. 이 함수는 설치 응용 프로그램 에서만에서 호출 되어야 합니다.  
  
 **SQLRemoveDriverManager** 핵심 구성 요소 사용 수가 1 씩 감소 됩니다. 구성 요소 사용 횟수가 0이 되 면 항목 시스템 정보를 제거 됩니다. 핵심 구성 요소 항목은 "ODBC 핵심" 제목 아래에 있는 시스템 정보를 다음 위치에서:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  구성 요소 사용 횟수 및 파일 사용 횟수가 0에 도달 하면 응용 프로그램 드라이버 관리자 파일을 물리적으로 제거 되지 해야 합니다.  
  
 **SQLRemoveDriverManager** 실제로 파일을 제거 하지 않습니다. 호출 프로그램이 파일을 삭제 하는 일을 담당 하 고 계산 파일 사용을 유지 관리 합니다. 하지만 드라이버 관리자 파일 안, 파일 사용 횟수를 증가 있어야 하는 다른 응용 프로그램에서 이러한 파일을 사용할 수 있으므로 구성 요소 사용 횟수 및 파일 사용 횟수가 0에 도달한 경우 제거할 수 있습니다.  
  
 **SQLRemoveDriverManager** 제거 프로세스의 일부로 호출 됩니다. ODBC 핵심 구성 요소 (드라이버 관리자, 커서 라이브러리, 설치 관리자, 언어 라이브러리, 관리자, 썽킹 파일 및 등 포함)을 전체적으로 제거 됩니다. 다음 파일을 제거 하는 경우 **SQLRemoveDriverManager** 제거 프로세스의 일부로 호출 됩니다.  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32.DLL|  
|ODBCCR32.DLL|ODBC16GT.DLL|  
|ODBCCU32.DLL|ODBC32GT.DLL|  
|ODBCINT 합니다. DLL|DS16GT.DLL|  
|ODBCTRAC 합니다. DLL|DS32GT.DLL|  
|MSVCRT40.DLL|ODBCAD32.EXE|  
|ODBCCP32.CPL||  
  
 **SQLRemoveDriverManager** 업그레이드 프로세스의 일부로 라고 합니다. 응용 프로그램에서 업그레이드를 수행 하는 것을 이전에 설치 하 고 드라이버를 발견 하면 드라이버를 제거 하 고 다시 설치 해야 합니다.  
  
 **SQLRemoveDriverManager** 구성 요소 사용 횟수를 감소 시키기 위해 먼저 호출 해야 합니다. **SQLInstallDriverEx** 다음 구성 요소 사용 횟수를 증가 시킬 호출 해야 합니다. 응용 프로그램 설치 프로그램을 새 파일로 이전 핵심 구성 요소 파일을 대체 해야 합니다. 파일 사용 횟수를 동일 하 게 유지 됩니다 및 이전 버전 핵심 구성 요소 파일을 사용 하는 다른 응용 프로그램에서 이제 최신 버전 파일을 사용 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|드라이버 관리자 설치|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
