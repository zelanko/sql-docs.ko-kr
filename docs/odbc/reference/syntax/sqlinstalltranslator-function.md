---
title: SQLInstallTranslator 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslator
helpviewer_keywords:
- SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5b973332c2fe0fa541635d326a3a5adecf6ae91
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076110"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 함수
**규칙**  
 소개 된 버전: ODBC 2.5, 사용 되지 않음  
  
 **요약**  
 ODBC 3.0에서는 **Sqlinstalltranslator** 가 [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)로 대체 되었습니다. **Sqlinstalltranslator** 에 대 한 호출은 **SQLInstallTranslatorEx**에 매핑됩니다. 자세한 내용은 **SQLInstallTranslatorEx**를 참조 하세요.  
  
 응용 프로그램에서 *lpszInfFile* 인수가 NULL이 아닌 값으로 설정 *된 ODBC 3.x* 드라이버 관리자에서 호출 하는 경우 **sqlinstalltranslator** 는 FALSE를 반환 합니다. *Odbc 2.x* 에서 사용 되는 odbc .inf 파일은 이전 버전과의 호환성을 위해서도 *odbc 3.x*에서 더 이상 지원 되지 않습니다.
