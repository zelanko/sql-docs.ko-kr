---
title: SQLPostInstallerError 함수 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306894"
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 함수
**규칙**  
 소개 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLPostInstallerError** 는 드라이버 또는 번역기 설치 라이브러리에서 **configdriver**, **ConfigDSN**및 **configdriver** 함수에 대 한 오류를 설치 관리자 오류 큐에 보고 하는 메커니즘을 제공 합니다. 응용 프로그램은이 API를 사용 하지 않습니다. **SQLInstallerError** 를 사용 하 여 오류를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>인수  
 *fErrorCode*  
 입력 설치 관리자 오류 코드입니다.  
  
 *szErrorMsg*  
 입력 오류 메시지 텍스트입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS 또는 SQL_ERROR.  
  
## <a name="diagnostics"></a>진단  
 **SQLPostInstallerError** 는 자체에 대 한 오류 값을 게시 하지 않습니다. 오류가 설치 관리자 오류 큐에 성공적으로 게시 된 경우 ( **SQLInstallerError**를 사용 하 여 검색할 수 있는 경우) SQL_SUCCESS 반환 됩니다. *Dwerrorcode* 인수의 값이 지정 된 설치 관리자 오류 코드 중 하나가 아닌 경우 SQL_ERROR 반환 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|드라이버 추가, 수정 또는 제거|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|데이터 원본 추가, 수정 또는 제거|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|변환 옵션 설정|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
