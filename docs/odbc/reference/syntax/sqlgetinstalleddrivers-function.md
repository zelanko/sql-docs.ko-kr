---
title: "SQLGetInstalledDrivers 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d2cd00f7306c7c9b6d60ff71d051b4709d7b3889
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 함수
**규칙**  
 ODBC 1.0 도입 된 버전:  
  
 **요약**  
 **SQLGetInstalledDrivers** 시스템 정보 [ODBC Drivers] 섹션을 읽고 설명에 설치 된 드라이버의 목록을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>인수  
 *lpszBuf*  
 [출력] 설치 된 드라이버의 설명의 목록입니다. 목록 구조에 대 한 내용은 "설명"을 참조 하십시오.  
  
 *cbBufMax*  
 [입력] 길이 *lpszBuf*합니다.  
  
 *pcbBufOut*  
 [출력] 총 바이트 수 (null 종료 바이트 제외)에서 반환 된 *lpszBuf*합니다. 보다 크거나 반환에 사용할 수 있는 바이트 수가 *cbBufMax*에서 드라이버 설명 목록이 *lpszBuf* 잘립니다 *cbBufMax* 빼기는 null 종료 문자입니다. *pcbBufOut* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetInstalledDrivers** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*lpszBuf* 인수는 NULL 이거나 잘못 된 또는 *cbBufMax* 0 보다 작거나 같은 인수 했습니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|구성 요소 레지스트리에서 찾을 수 없습니다|설치 관리자 레지스트리에 [ODBC Drivers] 섹션을 찾을 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>설명  
 각 드라이버 설명 null 바이트를으로 종료 되 고 전체 목록을 바이트 null로 종료 됩니다. (즉, 두 개의 null 바이트의 끝을 표시 목록입니다.) 할당된 된 버퍼를 전체 목록을 저장할 수 있을 만큼 큰 없으면 목록 오류 없이 잘립니다. Null 포인터로 전달 되는 경우 오류가 반환 됩니다 *lpszBuf*합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|드라이버 설명 및 특성을 반환합니다.|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|

