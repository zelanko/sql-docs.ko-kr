---
title: SQLRemoveTranslator 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 348d2c5da0731ba88ccd4dd6406d3754890f7906
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301790"
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 함수
**규칙**  
 버전 출시: ODBC 3.0  
  
 **요약**  
 **SQLRemoveTranslator는** 시스템 정보의 Odbcinst.ini 섹션에서 번역기에 대한 정보를 제거하고 번역자의 구성 요소 사용 수를 1로 감소시입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *lpsz번역기*  
 [입력] 시스템 정보의 Odbcinst.ini 키에 등록된 번역기의 이름입니다.  
  
 *lpdw사용계산*  
 [출력] 이 함수가 호출된 후 변환기의 사용 횟수입니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다. 이 함수를 호출할 때 시스템 정보에 항목이 없으면 함수는 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLRemoveTranslator** FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 관련 된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|레지스트리에서 구성 요소를 찾을 수 없습니다.|설치 관리자는 레지스트리에 없거나 레지스트리에서 찾을 수 없기 때문에 변환기 정보를 제거할 수 없습니다.|  
|ODBC_ERROR_INVALID_NAME|잘못된 드라이버 또는 번역기 이름|*lpszTranslator* 인수가 잘못되었습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|구성 요소 사용량 수를 증가하거나 감소시킬 수 없습니다.|설치 프로그램이 드라이버의 사용 횟수를 감소시키지 못했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLRemoveTranslator는** [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) 함수를 보완하고 시스템 정보의 구성 요소 사용 수를 업데이트합니다. 이 함수는 설치 응용 프로그램에서만 호출해야 합니다.  
  
 **SQLRemoveTranslator는** 구성 요소 사용 수를 1로 줄입니다. 구성 요소 사용 수가 0으로 이동하면 시스템 정보의 번역기 항목이 제거됩니다. 번역기 항목은 시스템 정보의 다음 위치에 있으며, 번역기 이름 아래:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator실제로** 어떤 파일을 제거하지 않습니다. 호출 프로그램은 파일을 삭제하고 파일 사용 수를 유지 관리합니다. 구성 요소 사용량 수와 파일 사용량 수가 0에 도달한 후에만 파일이 물리적으로 삭제됩니다. 구성 요소의 일부 파일은 삭제할 수 있으며 다른 파일은 파일 사용량 수를 증가시킨 다른 응용 프로그램에서 파일을 사용하는지 여부에 따라 삭제되지 않습니다.  
  
 **SQLRemoveTranslator는** 업그레이드 프로세스의 일부로 호출됩니다. 응용 프로그램이 업그레이드를 수행해야 하고 이전에 드라이버를 설치한 것을 감지한 경우 드라이버를 제거한 다음 다시 설치해야 합니다. **SQLRemoveTranslator** 먼저 구성 요소 사용 수를 감소 하기 위해 호출 해야 하 고 **SQLInstallTranslatorEx** 구성 요소 사용 수를 증가 하도록 호출 해야 합니다. 응용 프로그램 설치 프로그램은 이전 파일을 새 파일로 물리적으로 바꿔야 합니다. 파일 사용 수는 동일하게 유지되며 이전 버전 파일을 사용하는 다른 응용 프로그램은 이제 최신 버전을 사용합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|번역기 설치|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
