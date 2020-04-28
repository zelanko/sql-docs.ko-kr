---
title: Sql유효한 Dsn 함수 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286973"
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 함수
**규칙**  
 소개 된 버전: ODBC 2.0  
  
 **요약**  
 **Sql유효한 dsn** 은 이름이 시스템 정보에 추가 되기 전에 데이터 원본 이름의 길이와 유효성을 검사 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDSN*  
 입력 검사할 데이터 원본 이름입니다.  
  
## <a name="returns"></a>반환  
 함수는 데이터 원본 이름이 유효한 경우 TRUE를 반환 합니다. 데이터 원본 이름이 잘못 되었거나 함수 호출이 실패 한 경우 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **Sql유효한 dsn** 이 FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. PfErrorCode는 함수 호출이 실패 한 경우에만 반환 됩니다. 데이터 원본 이름이 잘못 되어 FALSE가 반환 된 경우에만 반환 됩니다. * \** 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **Sql올바른지 dsn** 은 데이터 원본 이름의 길이와 데이터 원본 이름의 개별 문자에 대 한 유효성을 검사 하기 위해 드라이버의 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) 에서 호출 됩니다. Sqlext에 정의 된 대로 이름의 길이가 SQL_MAX_DSN_LENGTH 보다 큰지 여부를 확인 합니다. 데이터 원본 이름의 길이는 [Sqlwritedsntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)에서도 확인 됩니다. **Sqlinvalid dsn** 은 데이터 원본 이름에 다음의 잘못 된 문자가 포함 되어 있는지 여부를 확인 합니다.  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|데이터 원본 추가, 수정 또는 제거|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (설치 DLL)|  
|데이터 원본 추가, 수정 또는 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|시스템 정보에 데이터 원본 이름 쓰기|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
