---
title: SQLValidDSN 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLValidDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLValidDSN
helpviewer_keywords:
- SQLValidDSN [ODBC]
ms.assetid: 930d1d89-337a-4429-85a2-84ee10555ac9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6dfafca22d0b04f2147b1af24b53e787493efe67
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286973"
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 함수
**규칙**  
 버전 출시: ODBC 2.0  
  
 **요약**  
 **SQLValidDSN은** 이름이 시스템 정보에 추가되기 전에 데이터 원본 이름의 길이와 유효성을 검사합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDSN*  
 [입력] 검사할 데이터 원본 이름입니다.  
  
## <a name="returns"></a>반환  
 데이터 원본 이름이 유효한 경우 함수는 TRUE를 반환합니다. 데이터 원본 이름이 잘못되었거나 함수 호출이 실패한 경우 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLValidDSNFALSE를** 반환 하는 경우 **SQLInstallerError**를 호출 하 여 관련 된 * \*pfErrorCode* 값을 가져올 수 있습니다. pfErrorCode는 함수 호출이 실패한 경우에만 반환되며 데이터 원본 이름이 잘못되었기 때문에 FALSE가 반환된 경우는 반환되지 않습니다. * \** 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLValidDSN은** 데이터 원본 이름의 길이와 데이터 원본 이름의 개별 문자의 유효성을 확인하기 위해 드라이버의 [ConfigDSN에](../../../odbc/reference/syntax/configdsn-function.md) 의해 호출됩니다. Sqlext.h에 정의된 대로 이름의 길이가 SQL_MAX_DSN_LENGTH 보다 큰지 여부를 확인합니다. (데이터 원본 이름의 길이는 [SQLWriteDSNToIni에](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)의해 확인됩니다.) **SQLValidDSN은** 다음 유효하지 않은 문자가 데이터 원본 이름에 포함되어 있는지 여부를 확인합니다.  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|데이터 원본 추가, 수정 또는 제거|[구성DSN(설치](../../../odbc/reference/syntax/configdsn-function.md) DLL)|  
|데이터 원본 추가, 수정 또는 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|시스템 정보에 데이터 원본 이름 작성|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
