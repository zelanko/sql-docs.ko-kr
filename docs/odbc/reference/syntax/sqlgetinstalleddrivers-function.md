---
title: SQLGetInstalledDriver 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInstalledDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInstalledDrivers
helpviewer_keywords:
- SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24793473bf4f25253ac11673df852d10cfb2c558
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303330"
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 함수
**규칙**  
 버전 출시: ODBC 1.0  
  
 **요약**  
 **SQLGetInstalledDriver는** 시스템 정보의 [ODBC 드라이버] 섹션을 읽고 설치된 드라이버에 대한 설명 목록을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>인수  
 *lpszBuf*  
 [출력] 설치된 드라이버에 대한 설명 목록입니다. 목록 구조에 대한 자세한 내용은 "주석"을 참조하십시오.  
  
 *cbBufMax*  
 [입력] *lpszBuf의*길이 .  
  
 *pcbBufOut*  
 [출력] *lpszBuf로*반환된 총 바이트 수(널 종료 바이트 제외). 반환할 수 있는 바이트 수가 *cbBufMax보다*크거나 같으면 *lpszBuf의* 드라이버 설명 목록이 *cbBufMax에서* null 종료 문자를 뺀 값으로 잘립니다. *pcbBufOut* 인수는 null 포인터일 수 있습니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetInstalledDriver** false를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 관련 된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못된 버퍼 길이|*lpszBuf* 인수가 NULL이거나 유효하지 않거나 *cbBufMax* 인수가 0보다 적거나 같습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|레지스트리에서 구성 요소를 찾을 수 없습니다.|설치 프로그램이 레지스트리에서 [ODBC 드라이버] 섹션을 찾을 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 각 드라이버 설명은 null 바이트로 종료되고 전체 목록은 null 바이트로 종료됩니다. 즉, 두 개의 null 바이트가 목록의 끝을 표시합니다. 할당된 버퍼가 전체 목록을 보유할 만큼 크지 않으면 목록의 오류 없이 잘립니다. null 포인터가 *lpszBuf로*전달되면 오류가 반환됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|드라이버 설명 및 특성 반환|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
