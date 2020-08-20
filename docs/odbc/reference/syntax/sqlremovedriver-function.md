---
description: SQLRemoveDriver 함수
title: SQLRemoveDriver 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriver
helpviewer_keywords:
- SQLRemoveDriver function [ODBC]
ms.assetid: 9a3b4f8b-982b-44b9-ade6-754ff026dc90
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 503fadfae168a2fc7259cd0507b283563d681bf7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487071"
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 함수
**규칙**  
 소개 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLRemoveDriver** 시스템 정보의 Odbcinst.ini 항목에서 드라이버에 대 한 정보를 변경 하거나 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDriver*  
 입력 시스템 정보의 Odbcinst.ini 키에 등록 된 드라이버의 이름입니다.  
  
 *fRemoveDSN*  
 입력 유효한 값은 다음과 같습니다.  
  
 TRUE: *lpszDriver*에 지정 된 드라이버와 연결 된 Dsn을 제거 합니다. FALSE: *lpszDriver*에 지정 된 드라이버와 연결 된 dsn을 제거 하지 않습니다.  
  
 *lpdwUsageCount*  
 출력 이 함수가 호출 된 후의 드라이버 사용 횟수입니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다. 이 함수가 호출 될 때 시스템 정보에 항목이 없으면 함수는 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLRemoveDriver** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \* pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \* pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|레지스트리에서 구성 요소를 찾을 수 없음|레지스트리에 없거나 레지스트리에서 찾을 수 없기 때문에 설치 관리자가 드라이버 정보를 제거할 수 없습니다.|  
|ODBC_ERROR_INVALID_NAME|드라이버 또는 번역기 이름이 잘못 되었습니다.|*LpszDriver* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|구성 요소 사용 횟수를 증가 시키거나 감소 시킬 수 없습니다.|드라이버의 사용 횟수를 감소 시 설치 관리자가 실패 했습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청 실패|*FRemoveDSN* 인수는 TRUE입니다. 그러나 하나 이상의 Dsn을 제거할 수 없습니다. ODBC_REMOVE_DRIVER 요청과 함께 **SQLConfigDriver** 를 호출 하지 못했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLRemoveDriver** 는 [Sqlinstalldriverex](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) 함수를 보완 하 고 시스템 정보의 구성 요소 사용 횟수를 업데이트 합니다. 이 함수는 설치 응용 프로그램 에서만 호출 해야 합니다.  
  
 **SQLRemoveDriver** 는 구성 요소 사용 횟수 값을 1 씩 감소 시킵니다. 구성 요소 사용 횟수가 0이 되 면 다음이 발생 합니다.  
  
1.  ODBC_REMOVE_DRIVER 옵션이 있는 **SQLConfigDriver** 함수가 호출 됩니다. *FRemoveDSN* 옵션이 TRUE로 설정 된 경우 **ConfigDSN** 함수는 **SQLRemoveDSNFromIni** 를 호출 하 여 lpszDriver에 지정 된 드라이버와 연결 된 모든 데이터 원본을 제거 *합니다.* *FRemoveDSN* 옵션을 FALSE로 설정 하면 데이터 원본이 삭제 되지 않습니다.  
  
2.  시스템 정보의 드라이버 항목이 제거 됩니다. 드라이버 항목은 드라이버 이름 아래에 다음과 같은 시스템 정보 위치에 있습니다.  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver** 는 실제로 파일을 제거 하지 않습니다. 호출 프로그램은 파일을 삭제 하 고 파일 사용 횟수를 유지 관리 하는 일을 담당 합니다. 구성 요소 사용 횟수와 파일 사용 횟수가 0에 도달 하 고 나면 파일이 실제로 삭제 됩니다. 파일 사용 횟수를 증가 시킨 다른 응용 프로그램에서 파일을 사용 하는지 여부에 따라 구성 요소의 일부 파일을 삭제할 수 있으며 다른 파일은 삭제 되지 않습니다.  
  
 **SQLRemoveDriver** 는 업그레이드 프로세스의 일부로도 호출 됩니다. 응용 프로그램에서 업그레이드를 수행 해야 하는 것을 감지 하 고 이전에 드라이버를 설치한 경우 드라이버를 제거한 후 다시 설치 해야 합니다. 구성 요소 사용 횟수를 감소 시키려면 **SQLRemoveDriver** 를 먼저 호출 해야 합니다. 그런 다음 **Sqlinstalldriverex** 를 호출 하 여 구성 요소 사용 횟수를 증가 시켜야 합니다. 응용 프로그램 설치 프로그램에서 이전 파일을 새 파일로 바꾸어야 합니다. 파일 사용 횟수는 동일 하 게 유지 되 고 이전 버전 파일을 사용 하는 다른 응용 프로그램은 이제 최신 버전을 사용 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|드라이버 추가, 수정 또는 제거|[Configdriver](../../../odbc/reference/syntax/configdriver-function.md) (설치 DLL)|  
|드라이버 추가, 수정 또는 제거|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|드라이버 설치|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
