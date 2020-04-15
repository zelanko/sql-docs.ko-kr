---
title: SQLRemoveDSNIni 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 848e82741954ab24941d5d519699292727ca25d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301802"
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 함수
**규칙**  
 버전 출시: ODBC 1.0  
  
 **요약**  
 **SQLRemoveDSNFromIni는** 시스템 정보에서 데이터 원본을 제거합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDSN*  
 [입력] 제거할 데이터 원본의 이름입니다.  
  
## <a name="returns"></a>반환  
 이 함수는 데이터 원본을 제거하거나 데이터 원본이 Odbc.ini 파일에 없는 경우 TRUE를 반환합니다. 데이터 원본을 제거하지 못하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLRemoveDSNFromIni가** FALSE를 반환하는 경우 **SQLInstaller Error**를 호출하여 연결된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_DSN|잘못된 DSN|*lpszDSN* 인수가 잘못되었습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청 실패|설치 프로그램이 레지스트리에서 DSN 정보를 제거할 수 없습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLRemoveDSNFromIni는** 시스템 정보의 [ODBC 데이터 원본] 섹션에서 데이터 원본 이름을 제거합니다. 또한 시스템 정보에서 데이터 원본 사양 섹션을 제거합니다.  
  
 이 함수는 드라이버 설정 라이브러리에서만 호출해야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|데이터 원본 추가, 수정 또는 제거|[구성DSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|데이터 원본 추가, 수정 또는 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|기본 데이터 원본 제거|[SQLRemoveDefault데이터 소스](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|시스템 정보에 데이터 원본 이름 추가|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
