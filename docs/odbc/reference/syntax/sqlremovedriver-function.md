---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 274451cdd2d1c3d811e4105a6d646044537999f1
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537371"
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 함수
**규칙**  
 도입 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLRemoveDriver** 변경 또는 시스템 정보 Odbcinst.ini 항목에서 드라이버에 대 한 정보를 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDriver*  
 [입력] 시스템 정보 Odbcinst.ini 키에 등록 하는 드라이버의 이름입니다.  
  
 *fRemoveDSN*  
 [입력] 유효한 값은:  
  
 TRUE: 제거에 지정 된 드라이버와 관련 된 Dsn *lpszDriver*합니다. FALSE: 에 지정 된 드라이버와 관련 된 Dsn을 제거 하지 마세요 *lpszDriver*합니다.  
  
 *lpdwUsageCount*  
 [출력] 이 함수를 호출한 후 드라이버의 사용 횟수입니다.  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다. 이 함수가 호출 될 때 시스템 정보에 없는 항목이 있으면 함수는 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLRemoveDriver** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|레지스트리에서 찾을 수 없습니다 하는 구성 요소|설치 관리자에 레지스트리에 없습니다. 또는 레지스트리에서 찾을 수 없습니다 때문에 드라이버 정보를 제거 하지 못했습니다.|  
|ODBC_ERROR_INVALID_NAME|잘못 된 드라이버 또는 변환기 이름|합니다 *lpszDriver* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|증가 또는 구성 요소 사용 횟수를 감소 시킬 수 없습니다.|설치 관리자는 드라이버의 사용 횟수를 감소 하지 않습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청이 실패 했습니다.|합니다 *fRemoveDSN* 인수가 TRUE; 그러나 하나 이상의 Dsn 제거할 수 없습니다. 에 대 한 호출 **SQLConfigDriver** ODBC_REMOVE_DRIVER 요청 하지 못했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 **SQLRemoveDriver** 보완 합니다 [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) 시스템 정보에는 구성 요소 사용을 계산 함수 및 업데이트 합니다. 이 함수는 설치 응용 프로그램 에서만에서 호출 되어야 합니다.  
  
 **SQLRemoveDriver** 구성 요소 사용 개수 값을 1 씩 감소 됩니다. 구성 요소 사용 횟수가 0이 되 면 하는 경우 다음이 발생 합니다.  
  
1.  합니다 **SQLConfigDriver** ODBC_REMOVE_DRIVER 옵션을 사용 하 여 함수가 호출 됩니다. 경우는 *fRemoveDSN* 옵션을 TRUE로 설정 합니다 **ConfigDSN** 함수 호출 **SQLRemoveDSNFromIni** 에 지정 된 드라이버와 관련 된 모든 데이터 원본을 제거 하려면 *lpszDriver 합니다.* 경우는 *fRemoveDSN* 옵션이 FALSE로 설정 되어, 데이터 원본 삭제 되지 것입니다.  
  
2.  시스템 정보에 드라이버 항목이 제거 됩니다. 드라이버 항목은 다음 시스템 위치에 있는 정보, 드라이버 이름:  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver** 실제로 파일을 제거 하지 않습니다. 호출 프로그램이 파일을 삭제 한 파일 사용 횟수를 유지 관리 하는 일을 담당 합니다. 구성 요소 사용 횟수 및 파일 사용 횟수에 도달한 후에 0 파일이 물리적으로 삭제 됩니다. 구성 요소에서 일부 파일을 삭제할 수 있습니다, 그리고 및 다른 사용자가 삭제 되지 파일 사용 횟수를 증가 하는 다른 응용 프로그램에서 파일의 사용 여부에 따라 합니다.  
  
 **SQLRemoveDriver** 업그레이드 프로세스의 일부로 라고 합니다. 응용 프로그램에서 업그레이드를 수행 하는 것을 이전에 설치 하 고 드라이버를 발견 하면 드라이버를 제거 하 고 다시 설치 해야 합니다. **SQLRemoveDriver** 구성 요소 사용 횟수를 감소 시키기 위해 먼저 호출 해야 차례로 **SQLInstallDriverEx** 구성 요소 사용 횟수를 증가 시킬를 호출 해야 합니다. 응용 프로그램 설치 프로그램을 새 파일로 이전 버전의 파일을 대체 해야 합니다. 파일 사용 횟수를 동일 하 게 유지 됩니다 및 이전 버전 파일을 사용 하는 다른 응용 프로그램은 이제 사용 하 여 최신 버전입니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 드라이버를 제거 합니다.|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) (에 DLL 설치)|  
|추가, 수정 또는 드라이버를 제거 합니다.|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|드라이버 설치|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
