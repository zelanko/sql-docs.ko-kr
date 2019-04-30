---
title: SQLValidDSN 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb490b475c5795125d11915729693eb630934eb8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233484"
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 함수
**규칙**  
 도입 된 버전: ODBC 2.0  
  
 **요약**  
 **SQLValidDSN** 이름을 시스템 정보에 추가 되기 전에 길이 데이터 원본 이름의 유효성을 검사 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDSN*  
 [입력] 데이터 원본 검사할 이름입니다.  
  
## <a name="returns"></a>반환 값  
 데이터 원본 이름이 올바르면 TRUE를 반환 하는 함수입니다. 데이터 원본 이름이 올바르지 않거나 함수 호출이 실패 한 경우 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLValidDSN** 연결 된 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 있습니다 **SQLInstallerError**합니다. A  *\*pfErrorCode* 반환 됩니다만 함수 호출이 실패 한 경우 데이터 원본 이름이 유효 하지 않으므로 FALSE를 반환 하는 경우에 없습니다. 다음 표에서  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 이 함수의 컨텍스트에서 각각 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생 했습니다에 대 한 특정 설치 관리자 오류가 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 관리자의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>주석  
 **SQLValidDSN** 드라이버를 호출한 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) 데이터 원본 이름의 길이 데이터 원본 이름에 각 문자의 유효성을 확인 합니다. 이름의 길이 보다 큰지 여부를 SQL_MAX_DSN_LENGTH, Sqlext.h에 정의 된 대로 확인 합니다. (데이터 원본 이름의 길이도 여 확인란이 [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md).) **SQLValidDSN** 다음 잘못 된 문자 데이터 원본 이름에 포함 되는지 여부를 확인 합니다.  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 데이터 원본 제거|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (에 DLL 설치)|  
|추가, 수정 또는 데이터 원본 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|시스템 정보를 데이터 원본 이름을 작성|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
