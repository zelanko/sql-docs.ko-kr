---
title: SQLRemoveTranslator 함수 | Microsoft Docs
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
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 495348c07ea707907f664358daea510951e7b208
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 함수
**규칙**  
 ODBC 3.0 도입 된 버전:  
  
 **요약**  
 **SQLRemoveTranslator** 정보가 제거는 변환기에 대 한 시스템 정보 및 감소의 Odbcinst.ini 섹션에서 변환기의 구성 요소 사용 횟수가 1 씩 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *lpszTranslator*  
 [입력] 시스템 정보 Odbcinst.ini 키에 등록 된 변환기의 이름입니다.  
  
 *lpdwUsageCount*  
 [출력] 이 함수를 호출한 후 변환기의 사용 횟수입니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다. 시스템 정보에 없는 항목이 있으면이 함수를 호출할 때 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLRemoveTranslator** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|구성 요소 레지스트리에서 찾을 수 없습니다|설치 관리자를 제거할 수 없습니다 변환기 정보 레지스트리에 없습니다. 또는 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_INVALID_NAME|잘못 된 드라이버 또는 변환기 이름입니다.|*lpszTranslator* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|증가 하거나 구성 요소 사용 횟수를 감소 시킬 수 없습니다.|드라이버의 사용 횟수를 감소 시키기 위해는 설치 프로그램이 실패 했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>설명  
 **SQLRemoveTranslator** 보완는 [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) 시스템 정보에는 구성 요소 사용을 계산 함수 및 업데이트 합니다. 이 함수는 설치 응용 프로그램 에서만에서 호출 되어야 합니다.  
  
 **SQLRemoveTranslator** 구성 요소의 사용 횟수가 1 씩 감소 됩니다. 구성 요소의 사용 횟수가 0이 되 면 시스템 정보에 변환기 항목 제거 됩니다. 변환기가 항목은 시스템 정보 변환기 이름 아래에 다음 위치에:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** 실제로 파일을 제거 하지 않습니다. 호출 프로그램은 파일을 삭제 하 고 파일 사용 횟수를 유지 관리 하는 일을 담당 합니다. 구성 요소 사용 횟수와 파일 사용 횟수에 도달한 후에 0이 파일이 물리적으로 삭제 됩니다. 다른 삭제 한 파일 사용 횟수를 증가 하는 다른 응용 프로그램에서 파일의 사용 여부에 따라 및 구성 요소에서 일부 파일을 삭제할 수 있습니다, 합니다.  
  
 **SQLRemoveTranslator** 업그레이드 프로세스의 일부로 라고도 합니다. 응용 프로그램 업그레이드를 수행 해야 하 고 드라이버가 이전에 설치한을 감지한 경우 드라이버를 제거 하 고 다시 설치 해야 합니다. **SQLRemoveTranslator** 구성 요소 사용 횟수를 감소 시키기 위해 먼저 호출 해야 하 고 다음 **SQLInstallTranslatorEx** 구성 요소 사용 수를 증가 호출 해야 합니다. 응용 프로그램 설치 프로그램을 새 파일로 이전 버전의 파일을 바꾸는 물리적으로 해야 합니다. 파일 사용 횟수 동일 하 게, 및 이전 버전 파일을 사용 하는 다른 응용 프로그램은 이제 사용 하 여 최신 버전입니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|설치 하는 변환기|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
