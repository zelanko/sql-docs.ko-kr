---
title: SQLWriteDSNToIni 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8eece6a1347aa7fba41577f66493e35f92a69d6f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039513"
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni 함수
**규칙**  
 소개 된 버전: ODBC 1.0  
  
 **요약**  
 **Sqlwritedsntoini** 는 시스템 정보에 데이터 원본을 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>인수  
 *lpszDSN*  
 입력 추가할 데이터 원본의 이름입니다.  
  
 *lpszDriver*  
 입력 실제 드라이버 이름 대신 사용자에 게 제공 되는 드라이버 설명 (일반적으로 연결 된 DBMS의 이름)입니다.  
  
## <a name="returns"></a>반환  
 이 함수는 성공 하면 TRUE를 반환 하 고 실패 하면 FALSE를 반환 합니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlwritedsntoini** 가 FALSE를 반환 하는 경우 **SQLInstallerError**를 호출 하 여 연결 된 * \*pfErrorCode* 값을 얻을 수 있습니다. 다음 표에서는 **SQLInstallerError** 에서 반환 될 수 있는 * \*pfErrorCode* 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|일반 설치 관리자 오류|특정 설치 관리자 오류가 없는 오류가 발생 했습니다.|  
|ODBC_ERROR_INVALID_DSN|잘못 된 DSN|*LpszDSN* 인수에 DSN에 대해 잘못 된 문자열이 포함 되어 있습니다.|  
|ODBC_ERROR_INVALID_NAME|드라이버 또는 번역기 이름이 잘못 되었습니다.|*LpszDriver* 인수가 잘못 되었습니다.|  
|ODBC_ERROR_REQUEST_FAILED|요청 실패|레지스트리에 DSN을 만들지 못했습니다.|  
|ODBC_ERROR_OUT_OF_MEM|메모리가 부족합니다.|메모리가 부족 하 여 설치 관리자가 함수를 수행할 수 없습니다.|  
  
## <a name="comments"></a>주석  
 **Sqlwritedsntoini** 는 시스템 정보의 [ODBC 데이터 원본] 섹션에 데이터 원본을 추가 합니다. 그런 다음 데이터 원본에 대 한 사양 섹션을 만들고 드라이버 DLL의 이름을 포함 하는 단일 키워드 (**드라이버**)를 해당 값으로 추가 합니다. 데이터 원본 사양 섹션이 이미 있는 경우 **Sqlwritedsntoini** 는 새 섹션을 만들기 전에 이전 섹션을 제거 합니다.  
  
 이 함수의 호출자는 시스템 정보의 데이터 원본 사양 섹션에 드라이버별 키워드 및 값을 추가 해야 합니다.  
  
 데이터 원본의 이름이 기본값 인 경우 **Sqlwritedsntoini** 는 시스템 정보에 기본 드라이버 사양 섹션도 만듭니다.  
  
 이 함수는 설치 DLL 에서만 호출 해야 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|데이터 원본 추가, 수정 또는 제거|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(설치 DLL)|  
|데이터 원본 추가, 수정 또는 제거|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|시스템 정보에서 데이터 원본 이름 제거|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
