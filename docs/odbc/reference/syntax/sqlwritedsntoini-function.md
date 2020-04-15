---
title: SQLWriteDSNToIni 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8bb141c8f54c49ca3a5c6fc4bc15d434f91795c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286963"
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni 함수
**규칙**  
 버전 출시: ODBC 1.0  
  
 **요약**  
 **SQLWriteDSNToIni는** 시스템 정보에 데이터 원본을 추가합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDSN*  
 [입력] 추가할 데이터 원본의 이름입니다.  
  
 *lpsz드라이버*  
 [입력] 실제 드라이버 이름 대신 사용자에게 표시되는 드라이버 설명(일반적으로 연결된 DBMS의 이름)입니다.  
  
## <a name="returns"></a>반환  
 함수는 성공하면 TRUE를 반환하고, 실패하면 FALSE를 반환합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLWriteDSNToIni가 FALSE를** 반환하는 경우 **SQLInstaller Error를**호출하여 연결된 * \*pfErrorCode* 값을 가져올 수 있습니다. 다음 표에는 **SQLInstallerError에서** 반환할 수 있는 * \*pfErrorCode* 값이 나열되어 있으며 이 함수의 컨텍스트에서 각 값을 설명합니다.  
  
|*\*pfErrorCode*|Error|설명|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생했습니다.|  
|ODBC_ERROR_INVALID_DSN|잘못된 DSN|*lpszDSN* 인수에는 DSN에 대해 유효하지 않은 문자열이 포함되어 있습니다.|  
|ODBC_ERROR_INVALID_NAME|잘못된 드라이버 또는 번역기 이름|*lpszDriver* 인수가 잘못되었습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청 실패|설치 프로그램이 레지스트리에서 DSN을 만들지 못했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리 부족으로 인해 설치 프로그램이 기능을 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **SQLWriteDSNToIni는** 시스템 정보의 [ODBC 데이터 원본] 섹션에 데이터 원본을 추가합니다. 그런 다음 데이터 원본에 대한 사양 섹션을 만들고 드라이버 DLL의 이름을 해당 값으로 사용하여 단일**키워드(Driver)를**추가합니다. 데이터 원본 사양 섹션이 이미 있는 경우 **SQLWriteDSNToIni는** 새 섹션을 만들기 전에 이전 섹션을 제거합니다.  
  
 이 함수의 호출자는 시스템 정보의 데이터 원본 사양 섹션에 드라이버별 키워드와 값을 추가해야 합니다.  
  
 데이터 원본의 이름이 기본값인 경우 **SQLWriteDSNToIni는** 시스템 정보의 기본 드라이버 사양 섹션도 만듭니다.  
  
 이 함수는 설치 DLL에서만 호출해야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|데이터 원본 추가, 수정 또는 제거|[구성DSN(설치](../../../odbc/reference/syntax/configdsn-function.md)DLL)|  
|데이터 원본 추가, 수정 또는 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|시스템 정보에서 데이터 원본 이름 제거|[SQLRemoveDSNIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
