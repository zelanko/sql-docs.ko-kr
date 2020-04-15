---
title: SQLInstallTranslator 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b094aa730fff6db80b9addb63a92bee0f5f85b2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300323"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 함수
**규칙**  
 버전 소개: ODBC 2.5, 더 이상 사용되지 않습니다.  
  
 **요약**  
 ODBC 3.0에서 **SQLInstallTranslator가** [SQLInstallTranslatorEx로](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)대체되었습니다. **SQLInstallTranslator에** 대한 호출은 **SQLInstallTranslatorEx에**매핑됩니다. 자세한 내용은 **SQLInstallTranslatorEx**를 참조하십시오.  
  
 **SQLInstallTranslator** 는 응용 프로그램이 NULL 이외의 값으로 설정된 *lpszInfFile* 인수를 사용하여 ODBC *3.x* 드라이버 관리자에서 호출하는 경우 FALSE를 반환합니다. ODBC *2.x에* 사용되는 Odbc.inf 파일은 이전 버전과의 호환성에서도 ODBC *3.x에서*더 이상 지원되지 않습니다.
