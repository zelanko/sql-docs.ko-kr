---
title: SQLPostInstallerError 함수 | Microsoft Docs
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
- SQLPostInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPostInstallerError
helpviewer_keywords:
- SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b34cef9e116bd75b5394cfe86e5f8784f0ff152
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 함수
**규칙**  
 ODBC 3.0 도입 된 버전:  
  
 **요약**  
 **SQLPostInstallerError** 드라이버 또는 변환기 설치 라이브러리에 대 한 오류 보고를 위한 메커니즘을 제공 된 **ConfigDriver**, **ConfigDSN**, 및 **ConfigTranslator**  installer 오류 큐에는 함수입니다. 응용 프로그램에이 API를 사용 하지 마십시오 사용할 **SQLInstallerError** 를 오류를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>인수  
 *fErrorCode*  
 [입력] Installer 오류 코드입니다.  
  
 *szErrorMsg*  
 [입력] 오류 메시지 텍스트입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS 또는 SQL_ERROR 합니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLPostInstallerError** 자체에 대 한 오류 값을 게시 하지 않습니다. 오류 installer 오류 큐에 성공적으로 게시 된 경우 (사용 하 여 검색할 수 **SQLInstallerError**), SQL_SUCCESS가 반환 됩니다. 경우 SQL_ERROR가 반환 됩니다에 있는 값의 *dwErrorCode* 인수는 지정 된 installer 오류 코드 중 하나가 아닙니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|추가, 수정 또는 드라이버를 제거 합니다.|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|추가, 수정 또는 데이터 원본 제거|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|변환 옵션 설정|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
