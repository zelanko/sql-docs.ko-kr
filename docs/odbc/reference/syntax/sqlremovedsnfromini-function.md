---
title: SQLRemoveDSNFromIni 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLRemoveDSNFromIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDSNFromIni
helpviewer_keywords:
- SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac2128424e1b48ecc82a0d0534db9222ad6ee734
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 함수
**규칙**  
 ODBC 1.0 도입 된 버전:  
  
 **요약**  
 **SQLRemoveDSNFromIni** 시스템 정보에서 데이터 원본을 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDSN*  
 [입력] 제거 하려면 데이터 원본의 이름입니다.  
  
## <a name="returns"></a>반환 값  
 함수는 데이터 원본이 제거 또는 데이터 원본 Odbc.ini 파일에 없습니다. 하는 경우 TRUE를 반환 합니다. 데이터 소스를 제거 하지 못하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLRemoveDSNFromIni** 관련 FALSE를 반환  *\*pfErrorCode* 호출 하 여 값을 얻을 수 **SQLInstallerError**합니다. 다음 표에  *\*pfErrorCode* 에서 반환 될 수 있는 값 **SQLInstallerError** 컨텍스트에서이 함수를 각각에 설명 합니다.  
  
|*\*pfErrorCode*|오류|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|오류가 발생에 대 한 셈이 특정 설치 관리자 오류가 있습니다.|  
|ODBC_ERROR_INVALID_DSN|잘못 된 DSN|*lpszDSN* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청이 실패 했습니다.|설치 관리자는 레지스트리에서 DSN 정보를 제거 하지 못했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|설치 프로그램의 메모리 부족으로 인해 함수를 수행할 수 있습니다.|  
  
## <a name="comments"></a>설명  
 **SQLRemoveDSNFromIni** 시스템 정보 [ODBC 데이터 소스] 섹션에서 데이터 원본 이름을 제거 합니다. 또한 시스템 정보를 데이터 원본 사양 섹션을 제거합니다.  
  
 이 함수는 드라이버 설치 라이브러리 에서만에서 호출 되어야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 데이터 원본 제거|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|추가, 수정 또는 데이터 원본 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|기본 데이터 원본 제거|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|시스템 정보에는 데이터 원본 이름 추가|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
