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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c94765dfe76bc5a1ef188328a6fe27e96671efb1
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363136"
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 함수
**규칙**  
 소개 된 버전: ODBC 3.0: Windows XP 서비스 팩 2, Windows Server 2003 서비스 팩 1 이상 운영 체제에서 사용 되지 않습니다.  
  
 **요약**  
 **SQLRemoveDriverManager** 시스템 정보의 Odbcinst.ini 항목에서 ODBC 핵심 구성 요소에 대 한 정보를 변경 하거나 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *pdwUsageCount*  
 출력 이 함수가 호출 된 후의 드라이버 관리자의 사용 횟수입니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다. 이 함수가 호출 될 때 시스템 정보에 항목이 없으면 함수는 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLRemoveDriverManager** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \* pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \* pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|레지스트리에서 구성 요소를 찾을 수 없음|레지스트리에 없거나 레지스트리에서 찾을 수 없기 때문에 설치 관리자가 드라이버 관리자 정보를 제거할 수 없습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|구성 요소 사용 횟수를 증가 시키거나 감소 시킬 수 없습니다.|드라이버 관리자의 사용 횟수를 감소 시 설치 관리자가 실패 했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리 부족|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>의견  
 **SQLRemoveDriverManager** 는 **Sqlinstalldrivermanager** 함수를 보완 하 고 시스템 정보의 구성 요소 사용 횟수를 업데이트 합니다. 이 함수는 설치 응용 프로그램 에서만 호출 해야 합니다.  
  
 **SQLRemoveDriverManager** 는 코어 구성 요소 사용 횟수를 1 씩 감소 시킵니다. 구성 요소 사용 횟수가 0이 되 면 항목 시스템 정보가 제거 됩니다. 핵심 구성 요소 항목은 시스템 정보에서 "ODBC Core" 제목의 다음 위치에 있습니다.  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  구성 요소 사용 횟수와 파일 사용 횟수가 0에 도달 하면 응용 프로그램에서 드라이버 관리자 파일을 물리적으로 제거 하면 안 됩니다.  
  
 **SQLRemoveDriverManager** 는 실제로 파일을 제거 하지 않습니다. 호출 프로그램은 파일을 삭제 하 고 파일 사용 횟수를 유지 관리 하는 일을 담당 합니다. 그러나 구성 요소 사용 횟수와 파일 사용 횟수가 0에 도달 하면 드라이버 관리자 파일이 제거 되어서는 안 됩니다. 이러한 파일은 파일 사용 횟수가 증가 하지 않은 다른 응용 프로그램에서 사용 될 수 있기 때문입니다.  
  
 **SQLRemoveDriverManager** 는 제거 프로세스의 일부로 호출 됩니다. ODBC 핵심 구성 요소 (드라이버 관리자, 커서 라이브러리, 설치 관리자, 언어 라이브러리, 관리자, 썽킹 파일 등 포함)는 전체적으로 제거 됩니다. **SQLRemoveDriverManager** 가 제거 프로세스의 일부로 호출 되는 경우 다음 파일은 제거 되지 않습니다.  

:::row:::
    :::column:::
        ODBC32DLL  
        ODBCCR32.DLL  
        ODBCCU32.DLL  
        ODBCINT.DLL  
        ODBCTRAC.DLL  
        MSVCRT40.DLL  
        ODBCCP32.CPL  
    :::column-end:::
    :::column:::
        ODBCCP32.DLL  
        ODBC16GT.DLL  
        ODBC32GT.DLL  
        DS16GT.DLL  
        DS32GT.DLL  
        ODBCAD32.EXE  
    :::column-end:::
:::row-end:::

 **SQLRemoveDriverManager** 는 업그레이드 프로세스의 일부로도 호출 됩니다. 응용 프로그램에서 업그레이드를 수행 해야 하는 것을 감지 하 고 이전에 드라이버를 설치한 경우 드라이버를 제거한 후 다시 설치 해야 합니다.  
  
 구성 요소 사용 횟수를 감소 시키려면 **SQLRemoveDriverManager** 를 먼저 호출 해야 합니다. 그런 다음 **Sqlinstalldriverex** 를 호출 하 여 구성 요소 사용 횟수를 증가 시켜야 합니다. 응용 프로그램 설치 프로그램은 이전 핵심 구성 요소 파일을 새 파일로 바꾸어야 합니다. 파일 사용 횟수는 동일 하 게 유지 되 고 이전 버전의 핵심 구성 요소 파일을 사용 하는 다른 응용 프로그램은 이제 최신 버전 파일을 사용 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|드라이버 관리자 설치|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
