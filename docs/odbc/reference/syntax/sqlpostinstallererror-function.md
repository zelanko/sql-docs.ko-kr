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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a189bd082bbf3d5f08080fccec48334165d5d15c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465318"
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 함수
**규칙**  
 도입 된 버전: ODBC 3.0  
  
 **요약**  
 **SQLPostInstallerError** 드라이버나 translator 설치 라이브러리에 대 한 오류 보고를 위한 메커니즘을 제공 합니다 **ConfigDriver**합니다 **ConfigDSN**, 및 **ConfigTranslator**  설치 관리자 오류 큐로 함수입니다. 이 API를 사용 하지 않는 응용 사용 하 여 **SQLInstallerError** 오류를 검색 하려면.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>인수  
 *fErrorCode*  
 [입력] 설치 관리자 오류 코드입니다.  
  
 *szErrorMsg*  
 [입력] 오류 메시지 텍스트입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS 또는 SQL_ERROR 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLPostInstallerError** 자체에 대 한 오류 값을 게시 하지 않습니다. 오류 설치 관리자 오류 큐에 성공적으로 게시 된 경우 (사용 하 여 검색 가능 **SQLInstallerError**), SQL_SUCCESS가 반환 됩니다. 경우 SQL_ERROR가 반환 됩니다의 값을 *dwErrorCode* 인수가 지정 된 설치 관리자 오류 코드 중 하나가 아닙니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 드라이버를 제거 합니다.|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|추가, 수정 또는 데이터 원본 제거|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|변환 옵션 설정|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
