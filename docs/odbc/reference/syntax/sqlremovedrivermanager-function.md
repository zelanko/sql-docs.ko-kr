---
title: SQLRemoveDriverManager 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad7508ef6825bda50adee02fe92665e4d3445ee5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 함수
**규칙**  
 버전 소개: ODBC 3.0: Windows XP 서비스 팩 2, Windows Server 2003 서비스 팩 1 및 이상의 운영 체제에서 사용 되지 않습니다.  
  
 **요약**  
 **SQLRemoveDriverManager** 변경 되거나 Odbcinst.ini 항목 시스템 정보에서 ODBC 핵심 구성 요소에 대 한 정보를 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *pdwUsageCount*  
 [출력] 드라이버 관리자의이 함수를 호출한 후 사용 횟수입니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다. 시스템 정보에 없는 항목이 있으면이 함수를 호출할 때 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLRemoveDriverManager** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|구성 요소 레지스트리에서 찾을 수 없습니다|설치 관리자에 레지스트리에 없습니다. 되었거나 레지스트리에서 찾을 수 없습니다 드라이버 관리자 정보를 제거 하지 못했습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|증가 하거나 구성 요소 사용 횟수를 감소 시킬 수 없습니다.|드라이버 관리자의 사용 횟수를 감소 시키기 위해는 설치 프로그램이 실패 했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>설명  
 **SQLRemoveDriverManager** 보완는 **SQLInstallDriverManager** 함수 및 시스템 정보에는 구성 요소 사용을 계산 하는 업데이트 합니다. 이 함수는 설치 응용 프로그램 에서만에서 호출 되어야 합니다.  
  
 **SQLRemoveDriverManager** 핵심 구성 요소 사용 횟수가 1 씩 감소 됩니다. 구성 요소의 사용 횟수가 0이 되 면 항목 시스템 정보 제거 됩니다. 핵심 구성 요소 항목은 시스템 정보 "ODBC 핵심" 제목 아래에 다음 위치에서:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  구성 요소 사용 수 및 파일 사용 횟수가 0에 도달 하면 응용 프로그램 파일 드라이버 관리자를 물리적으로 제거 하지 않아야 합니다.  
  
 **SQLRemoveDriverManager** 실제로 파일을 제거 하지 않습니다. 호출 프로그램 파일을 삭제 하는 것에 대 한 하며 파일 사용을 유지 관리를 계산 합니다. 하지만 드라이버 관리자 파일 되어서는 안, 파일 사용 횟수를 증가 있어야 하는 다른 응용 프로그램에서 이러한 파일을 사용할 수 있으므로 구성 요소 사용 수 및 파일 사용 횟수가 모두 0에 도달한 경우 제거할 수 있습니다.  
  
 **SQLRemoveDriverManager** 제거 프로세스의 일부로 호출 됩니다. ODBC 핵심 구성 요소 (드라이버 관리자, 커서 라이브러리, 설치 관리자, 언어 라이브러리, 관리자, 썽킹 파일, 및 등 포함)이 전체적으로 제거 됩니다. 다음 파일에 없는 될 때 제거 **SQLRemoveDriverManager** 제거 프로세스의 일부로 호출 됩니다.  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32 합니다. DLL|  
|ODBCCR32 합니다. DLL|ODBC16GT 합니다. DLL|  
|ODBCCU32 합니다. DLL|ODBC32GT 합니다. DLL|  
|ODBCINT 합니다. DLL|DS16GT 합니다. DLL|  
|ODBCTRAC 합니다. DLL|DS32GT 합니다. DLL|  
|MSVCRT40 합니다. DLL|ODBCAD32 합니다. EXE|  
|ODBCCP32 합니다. CPL||  
  
 **SQLRemoveDriverManager** 업그레이드 프로세스의 일부로 라고도 합니다. 응용 프로그램 업그레이드를 수행 해야 하 고 드라이버가 이전에 설치한을 감지한 경우 드라이버를 제거 하 고 다시 설치 해야 합니다.  
  
 **SQLRemoveDriverManager** 구성 요소 사용 횟수를 감소 시키기 위해 먼저 호출 해야 합니다. **SQLInstallDriverEx** 구성 요소 사용 횟수를 증가 시키는 다음 호출 해야 합니다. 응용 프로그램 설치 프로그램을 새 파일로 이전 핵심 구성 요소 파일을 바꿔야 합니다. 파일 사용 횟수는 동일 하 게 유지 됩니다 및 이전 버전 핵심 구성 요소 파일을 사용 하는 다른 응용 프로그램에서 최신 버전 파일을 사용 이제 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|드라이버 관리자 설치|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
