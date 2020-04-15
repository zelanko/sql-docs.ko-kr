---
title: SQL포스트설치자 오류 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPostInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPostInstallerError
helpviewer_keywords:
- SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cdceff5c4e175ba9f135c6e5e4405933b1a86b7c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306894"
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 함수
**규칙**  
 버전 출시: ODBC 3.0  
  
 **요약**  
 **SQLPostInstallerError는** 설치 프로그램 오류 큐에 **ConfigDriver,** **ConfigDSN**및 **ConfigTranslator** 함수에 대한 오류를 보고하는 드라이버 또는 번역기 설치 라이브러리에 대한 메커니즘을 제공합니다. 응용 프로그램은 이 API를 사용하지 않습니다. **SQLInstallerError를** 사용하여 오류를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>인수  
 *fErrorCode*  
 [입력] 설치 관리자 오류 코드입니다.  
  
 *szErrorMsg*  
 [입력] 오류 메시지 텍스트입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS 또는 SQL_ERROR.  
  
## <a name="diagnostics"></a>진단  
 **SQLPostInstallerError** 는 자체적으로 오류 값을 게시하지 않습니다. 설치 관리자 오류 큐에 오류가 성공적으로 게시된 **경우(SQLInstallerError를**사용하여 검색 가능) SQL_SUCCESS 반환됩니다. *dwErrorCode* 인수의 값이 지정된 설치 관리자 오류 코드 중 하나가 아닌 경우 SQL_ERROR 반환됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|드라이버 추가, 수정 또는 제거|[구성 드라이버](../../../odbc/reference/syntax/configdriver-function.md)|  
|데이터 원본 추가, 수정 또는 제거|[구성DSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|변환 옵션 설정|[콘피그 번역기](../../../odbc/reference/syntax/configtranslator-function.md)|
