---
title: SQLRemoveDriver 기능 | 마이크로 소프트 문서
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
ms.openlocfilehash: 205c5b46e5f6cea195094f7a50e81d7509927d1a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303934"
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 함수
**규칙**  
 버전 출시: ODBC 3.0  
  
 **요약**  
 **SQLRemoveDriver** 변경 하거나 시스템 정보의 Odbcinst.ini 항목에서 드라이버에 대 한 정보를 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *lpsz드라이버*  
 [입력] 시스템 정보의 Odbcinst.ini 키에 등록된 드라이버의 이름입니다.  
  
 *fRemoveDSN*  
 [입력] 유효한 값은 다음과 같습니다.  
  
 TRUE: *lpszDriver에*지정된 드라이버와 연결된 DSN을 제거합니다. FALSE: *lpszDriver에*지정된 드라이버와 연결된 DSN을 제거하지 마십시오.  
  
 *lpdw사용계산*  
 [출력] 이 함수가 호출된 후 드라이버의 사용 횟수입니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다. 이 함수를 호출할 때 시스템 정보에 항목이 없으면 함수는 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLRemoveDriver** FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 관련 된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|레지스트리에서 구성 요소를 찾을 수 없습니다.|설치 관리자는 레지스트리에 없거나 레지스트리에서 찾을 수 없기 때문에 드라이버 정보를 제거할 수 없습니다.|  
|ODBC_ERROR_INVALID_NAME|잘못된 드라이버 또는 번역기 이름|*lpszDriver* 인수가 잘못되었습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|구성 요소 사용량 수를 증가하거나 감소시킬 수 없습니다.|설치 프로그램이 드라이버의 사용 횟수를 감소시키지 못했습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청 실패|*fRemoveDSN* 인수는 TRUE였습니다. 그러나 하나 이상의 DSN을 제거할 수 없습니다. ODBC_REMOVE_DRIVER 요청이 있는 **SQLConfigDriver** 호출에 실패했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLRemoveDriver는** [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) 기능을 보완하고 시스템 정보의 구성 요소 사용 수를 업데이트합니다. 이 함수는 설치 응용 프로그램에서만 호출해야 합니다.  
  
 **SQLRemoveDriver는** 구성 요소 사용 개수 값을 1로 줄입니다. 구성 요소 사용 수가 0으로 이동하면 다음과 같은 일이 발생합니다.  
  
1.  ODBC_REMOVE_DRIVER 옵션이 있는 **SQLConfigDriver** 함수가 호출됩니다. *fRemoveDSN* 옵션이 TRUE로 설정된 경우 **ConfigDSN** 함수는 **SQLRemoveDSNFromIni를** 호출하여 *lpszDriver에* 지정된 드라이버와 관련된 모든 데이터 원본을 제거합니다. *fRemoveDSN* 옵션이 FALSE로 설정되어 있으면 데이터 원본이 삭제되지 않습니다.  
  
2.  시스템 정보의 드라이버 항목이 제거됩니다. 드라이버 항목은 드라이버 이름 아래 다음 시스템 정보 위치에 있습니다.  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver실제로** 어떤 파일을 제거 하지 않습니다. 호출 프로그램은 파일을 삭제하고 파일 사용 수를 유지 관리합니다. 구성 요소 사용량 수와 파일 사용량 수가 0에 도달한 후에만 파일이 물리적으로 삭제됩니다. 구성 요소의 일부 파일은 삭제할 수 있으며 다른 파일은 파일 사용량 수를 증가시킨 다른 응용 프로그램에서 파일을 사용하는지 여부에 따라 삭제되지 않습니다.  
  
 **SQLRemoveDriver는** 업그레이드 프로세스의 일부로호출됩니다. 응용 프로그램이 업그레이드를 수행해야 하고 이전에 드라이버를 설치한 것을 감지한 경우 드라이버를 제거한 다음 다시 설치해야 합니다. **SQLRemoveDriver** 먼저 구성 요소 사용 수를 감소 하기 위해 호출 해야 하 고 **SQLInstallDriverEx** 구성 요소 사용 수를 증가 하도록 호출 해야 합니다. 응용 프로그램 설치 프로그램은 이전 파일을 새 파일로 바꿔야 합니다. 파일 사용 수는 동일하게 유지되며 이전 버전 파일을 사용하는 다른 응용 프로그램은 이제 최신 버전을 사용합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|드라이버 추가, 수정 또는 제거|[구성 드라이버(설치](../../../odbc/reference/syntax/configdriver-function.md) DLL)|  
|드라이버 추가, 수정 또는 제거|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|드라이버 설치|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
