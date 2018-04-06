---
title: SQLGetTranslator 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLGetTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTranslator
helpviewer_keywords:
- SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0687666f81d30615a2cc94268ed861faf1031d8d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 함수
**규칙**  
 ODBC 2.0 도입 된 버전:  
  
 **요약**  
 **SQLGetTranslator** 사용자는 변환기를 선택할 수 있는 대화 상자가 표시 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLGetTranslator(  
     HWND      hwndParent,  
     LPSTR     lpszName,  
     WORD      cbNameMax,  
     WORD *    pcbNameOut,  
     LPSTR     lpszPath,  
     WORD      cbPathMax,  
     WORD *    pcbPathOut,  
     DWORD *   pvOption);  
```  
  
## <a name="arguments"></a>인수  
 *창은*  
 [입력] 부모 창 핸들입니다.  
  
 *lpszName*  
 [입력/출력] 시스템 정보에서 변환기의 이름입니다.  
  
 *cbNameMax*  
 [입력] 최대 길이 *lpszName* 버퍼입니다.  
  
 *pcbNameOut*  
 [입력/출력] 지났거나에 반환 된 바이트 (null 종료 바이트 제외)의 총 *lpszName*합니다. 보다 크거나 반환에 사용할 수 있는 바이트 수가 *cbNameMax*에서 변환기 이름을 *lpszName* 잘립니다 *cbNameMax* 빼기는 null 종료 문자입니다. *pcbNameOut* 인수는 null 포인터 일 수 있습니다.  
  
 *lpszPath*  
 [출력] 변환 DLL의 전체 경로입니다.  
  
 *cbPathMax*  
 [입력] 최대 길이 *lpszPath* 버퍼입니다.  
  
 *pcbPathOut*  
 [출력] 총 바이트 수 (null 종료 바이트 제외)에서 반환 된 *lpszPath*합니다. 보다 크거나 반환에 사용할 수 있는 바이트 수가 *cbPathMax*, 번역 DLL 경로에 *lpszPath* 잘립니다 *cbPathMax* 빼기는 null 종료 문자입니다. *pcbPathOut* 인수는 null 포인터 일 수 있습니다.  
  
 *pvOption*  
 [출력] 32 비트 번역 옵션입니다.  
  
## <a name="returns"></a>반환 값  
 함수 또는 경우에 성공이 고, FALSE 실패할 경우 대화 상자를 취소 하는 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetTranslator** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_INVALID_BUFF_LEN|잘못 된 버퍼 길이|*cbNameMax* 또는 *cbPathMax* 0 보다 작거나 같은 인수 했습니다.|  
|ODBC_ERROR_INVALID_HWND|잘못 된 창 핸들|*창은* 인수가 잘못 되었거나 NULL입니다.|  
|ODBC_ERROR_INVALID_NAME|잘못 된 드라이버 또는 변환기 이름입니다.|*lpszName* 인수가 잘못 되었습니다. 레지스트리에서 찾을 수 없습니다.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|드라이버 또는 변환기 설치 라이브러리를 로드할 수 없습니다.|변환기 라이브러리를 로드할 수 없습니다.|  
|ODBC_ERROR_INVALID_OPTION|잘못 된 트랜잭션 옵션|*pvOption* 인수에 잘못 된 값을 포함 합니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 경우 *창은* 은 null 이거나 *lpszName*, *lpszPath*, 또는 *pvOption* null 포인터가 **SQLGetTranslator** FALSE를 반환 합니다. 그렇지 않은 경우 다음 대화 상자에 설치 된 변환기 목록이 표시 됩니다.  
  
 ![변환기 대화 상자 선택](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 경우 *lpszName* 올바른 변환기 이름을 포함을 선택 합니다. 그렇지 않으면 \<아니요 변환기 >을 선택 합니다.  
  
 사용자가 선택 \<아니요 변환기 >, 내용의 *lpszName*, *lpszPath*, 및 *pvOption* 는 그대로 유지 합니다. **SQLGetTranslator** 설정 *pcbNameOut* 및 *pcbPathOut* 0과 TRUE 반환 합니다.  
  
 변환기를 선택 하는 사용자의 경우 **SQLGetTranslator** 호출 **ConfigTranslator** 변환기의 설치 프로그램 DLL에서에서 합니다. 경우 **ConfigTranslator** FALSE를 반환 **SQLGetTranslator** 는 대화 상자로 돌아갑니다. 경우 **ConfigTranslator** TRUE를 반환 하면 **SQLGetTranslator** 선택한 변환기 이름, 경로 및 변환 옵션에 따라 TRUE를 반환 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|변환기를 구성합니다.|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|번역 속성 가져오기|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|번역 속성 설정|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
