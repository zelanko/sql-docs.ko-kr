---
description: SQLRemoveTranslator 함수
title: SQLRemoveTranslator 함수 | Microsoft Docs
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
ms.openlocfilehash: 92042d1a29720d8fcca32d3fb7127f24a0566b7e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499606"
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 함수
**규칙**  
 소개 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLRemoveTranslator** 는 시스템 정보의 Odbcinst.ini 섹션에서 변환기에 대 한 정보를 제거 하 고 변환기의 구성 요소 사용 횟수를 1 씩 감소 시킵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>인수  
 *lpszTranslator*  
 입력 시스템 정보의 Odbcinst.ini 키에 등록 된 변환기의 이름입니다.  
  
 *lpdwUsageCount*  
 출력 이 함수가 호출 된 후의 변환기 사용 횟수입니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다. 이 함수가 호출 될 때 시스템 정보에 항목이 없으면 함수는 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLRemoveTranslator** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \* pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \* pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|오류|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|레지스트리에서 구성 요소를 찾을 수 없음|레지스트리에 없거나 레지스트리에서 찾을 수 없기 때문에 설치 관리자가 변환기 정보를 제거할 수 없습니다.|  
|ODBC_ERROR_INVALID_NAME|드라이버 또는 번역기 이름이 잘못 되었습니다.|*LpszTranslator* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|구성 요소 사용 횟수를 증가 시키거나 감소 시킬 수 없습니다.|드라이버의 사용 횟수를 감소 시 설치 관리자가 실패 했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLRemoveTranslator** 는 [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) 함수를 보완 하 고 시스템 정보의 구성 요소 사용 횟수를 업데이트 합니다. 이 함수는 설치 응용 프로그램 에서만 호출 해야 합니다.  
  
 **SQLRemoveTranslator** 는 구성 요소 사용 횟수를 1 씩 감소 시킵니다. 구성 요소 사용 횟수가 0으로 이동 하면 시스템 정보의 변환기 항목이 제거 됩니다. 변환기 항목은 시스템 정보에서 변환기 이름 아래에 있는 다음 위치에 있습니다.  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** 는 실제로 파일을 제거 하지 않습니다. 호출 프로그램은 파일을 삭제 하 고 파일 사용 횟수를 유지 관리 하는 일을 담당 합니다. 구성 요소 사용 횟수와 파일 사용 횟수가 0에 도달 하 고 나면 파일이 실제로 삭제 됩니다. 파일 사용 횟수를 증가 시킨 다른 응용 프로그램에서 파일을 사용 하는지 여부에 따라 구성 요소의 일부 파일을 삭제할 수 있으며 다른 파일은 삭제 되지 않습니다.  
  
 **SQLRemoveTranslator** 는 업그레이드 프로세스의 일부로도 호출 됩니다. 응용 프로그램에서 업그레이드를 수행 해야 하는 것을 감지 하 고 이전에 드라이버를 설치한 경우 드라이버를 제거한 후 다시 설치 해야 합니다. 구성 요소 사용 횟수를 감소 시키려면 **SQLRemoveTranslator** 를 먼저 호출한 다음 **SQLInstallTranslatorEx** 를 호출 하 여 구성 요소 사용 횟수를 증가 시켜야 합니다. 응용 프로그램 설치 프로그램은 이전 파일을 새 파일로 물리적으로 바꾸어야 합니다. 파일 사용 횟수는 동일 하 게 유지 되 고 이전 버전 파일을 사용 하는 다른 응용 프로그램은 이제 최신 버전을 사용 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|번역기 설치|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
