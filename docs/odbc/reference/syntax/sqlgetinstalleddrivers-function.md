---
title: SQLGetInstalledDrivers 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 093da37d061153013682772c3284e0afe88b7866
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618941"
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 함수
**규칙**  
 ODBC 도입 된 버전: 1.0  
  
 **요약**  
 **SQLGetInstalledDrivers** 시스템 정보 [ODBC Drivers] 섹션을 읽고 설치 된 드라이버의 설명의 목록을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>인수  
 *lpszBuf*  
 [출력] 설치 된 드라이버의 설명의 목록입니다. 목록 구조에 대 한 자세한 내용은 "설명입니다."을 참조 하세요.  
  
 *cbBufMax*  
 [입력] 길이가 *lpszBuf*합니다.  
  
 *pcbBufOut*  
 [출력] 총 바이트 (null 종료 바이트 제외)에서 반환 된 *lpszBuf*합니다. 반환할 사용 가능한 바이트 수가 보다 크거나 같은 경우 *cbBufMax*에서 드라이버 설명 목록을 *lpszBuf* 잘립니다 *cbBufMax* 빼기는 null 종료 문자입니다. 합니다 *pcbBufOut* 인수로 null 포인터를 사용할 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 함수가 성공적 이면 FALSE 실패 한 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetInstalledDrivers** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|합니다 *lpszBuf* 인수가 NULL 이거나 잘못 되었거나, 또는 *cbBufMax* 인수가 0 보다 작거나 합니다.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|레지스트리에서 찾을 수 없습니다 하는 구성 요소|설치 관리자 [ODBC Drivers] 섹션을 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 각 드라이버 설명을 null 바이트를 사용 하 여 종료 됩니다 하 고 전체 목록을 null 바이트를 사용 하 여 종료 됩니다. (즉, 두 개의 null 바이트의 끝을 표시 목록입니다.) 할당된 된 버퍼를 충분히 전체 목록을 저장할 수 없는 경우에 목록 오류 없이 잘립니다. Null 포인터를 전달 된 경우 오류가 반환 됩니다 *lpszBuf*합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|드라이버 설명 및 특성을 반환합니다.|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
