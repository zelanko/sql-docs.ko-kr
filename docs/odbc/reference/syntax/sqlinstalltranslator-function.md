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
manager: craigg
ms.openlocfilehash: 08a9e3a1afef8b9ea3bf1f4266196341e0edeb76
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792855"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 함수
**규칙**  
 도입 된 버전: ODBC 2.5에서는 사용 되지 않음  
  
 **요약**  
 ODBC 3.0에서 **SQLInstallTranslator** 바뀌었습니다 [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)합니다. 에 대 한 호출 **SQLInstallTranslator** 매핑될 **SQLInstallTranslatorEx**합니다. 자세한 내용은 **SQLInstallTranslatorEx**합니다.  
  
 **SQLInstallTranslator** 응용 프로그램에서 ODBC 호출 하는 경우 FALSE를 반환 *3.x* 사용 하 여 드라이버 관리자는 *lpszInfFile* 인수는 NULL이 아닌 값으로 설정 합니다. ODBC에서 사용한 Odbc.inf 파일은 *2.x* ODBC에서 더 이상 지원 되지 *3.x*이전 버전과 호환성을 위해서도 합니다.
