---
title: SQLWriteDSNToIni 함수 | Microsoft Docs
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
- SQLWriteDSNToIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteDSNToIni
helpviewer_keywords:
- SQLWriteDSNToIni [ODBC]
ms.assetid: dc7018b2-18d4-4657-96d0-086479a47474
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a1ee3bdbdc14c01bf267c9dbb64ef10c93dfe1a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni 함수
**규칙**  
 ODBC 1.0 도입 된 버전:  
  
 **요약**  
 **SQLWriteDSNToIni** 시스템 정보에는 데이터 소스를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDSN*  
 [입력] 추가할 데이터 원본의 이름입니다.  
  
 *lpszDriver*  
 [입력] 드라이버 설명 (일반적으로 연결된 되는 DBMS의 이름) 실제 드라이버 이름 대신 사용자에 게 표시 합니다.  
  
## <a name="returns"></a>반환 값  
 함수는 실패 한 경우, FALSE 실패할 경우 TRUE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLWriteDSNToIni** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_INVALID_DSN|잘못 된 DSN|*lpszDSN* 인수에는 DSN에 대 한 잘못 된 문자열이 포함 되어 있습니다.|  
|ODBC_ERROR_INVALID_NAME|잘못 된 드라이버 또는 변환기 이름입니다.|*lpszDriver* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청이 실패 했습니다.|설치 관리자를 레지스트리에서 DSN을 만들지 못했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>설명  
 **SQLWriteDSNToIni** 시스템 정보 [ODBC 데이터 소스] 섹션에 데이터 소스를 추가 합니다. 그런 다음 데이터 원본에 대 한 사양 섹션 만들고 추가 하는 단일 키워드 (**드라이버**) 드라이버의 값으로 DLL의 이름으로 합니다. 데이터 원본 사양 섹션에 이미 있으면 **SQLWriteDSNToIni** 새를 만들기 전에 이전 섹션을 제거 합니다.  
  
 이 함수의 호출자에 게는 모든 드라이버 관련 키워드와 값의 시스템 정보와 데이터 원본 사양 섹션에 추가 해야 합니다.  
  
 데이터 원본의 이름을 기본값이 면 **SQLWriteDSNToIni** 시스템 정보에도 기본 드라이버 사양 섹션을 만듭니다.  
  
 이 함수는 설치 DLL 에서만에서 호출 되어야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 데이터 원본 제거|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(에 DLL 설치)|  
|추가, 수정 또는 데이터 원본 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|시스템 정보에서 제거 하는 데이터 원본 이름|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
