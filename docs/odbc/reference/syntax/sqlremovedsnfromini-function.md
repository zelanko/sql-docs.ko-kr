---
title: SQLRemoveDSNFromIni 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4cc83a8cafffc9b5d1166df76d91ce4c63f0b858
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68024534"
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 함수
**규칙**  
 소개 된 버전: ODBC 1.0  
  
 **요약**  
 **SQLRemoveDSNFromIni** 는 시스템 정보에서 데이터 원본을 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDSN*  
 입력 제거할 데이터 원본의 이름입니다.  
  
## <a name="returns"></a>반환  
 함수는 데이터 원본을 제거 하거나 데이터 원본이 Odbc .ini 파일에 없는 경우 TRUE를 반환 합니다. 데이터 원본을 제거 하지 못한 경우 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLRemoveDSNFromIni** 가 FALSE를 반환 하면 **SQLInstallerError**을 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_DSN|잘못 된 DSN|*LpszDSN* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청 실패|레지스트리에서 DSN 정보를 제거할 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLRemoveDSNFromIni** 는 시스템 정보의 [ODBC 데이터 원본] 섹션에서 데이터 원본 이름을 제거 합니다. 또한 시스템 정보에서 데이터 원본 사양 섹션을 제거 합니다.  
  
 이 함수는 드라이버 설치 라이브러리 에서만 호출 해야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|데이터 원본 추가, 수정 또는 제거|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|데이터 원본 추가, 수정 또는 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|기본 데이터 소스 제거|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|시스템 정보에 데이터 원본 이름 추가|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
