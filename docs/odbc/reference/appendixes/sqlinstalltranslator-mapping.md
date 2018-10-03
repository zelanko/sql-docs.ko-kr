---
title: SQLInstallTranslator 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9760bfad769e9508d58d1cd00f98376dbd13d877
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831390"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 매핑
경우는 ODBC 2. *x* 응용 프로그램 호출 **SQLInstallTranslator** ODBC 3를 통해 *.x* 드라이버를 드라이버 관리자에 대 한 호출 매핑합니다 **SQLInstallTranslatorEx**. 응용 프로그램을 호출 하지 않아야 **SQLInstallTranslator** ODBC 3에서 *.x* 사용 하 여 드라이버 관리자는 *lpszInfFile* 인수는 NULL이 아닌 값으로 설정 합니다. ODBC입니다. ODBC 2에 사용 되는 INF 파일입니다. *x* ODBC 3에서 더 이상 지원 되지 *.x*이전 버전과 호환성을 위해서도 합니다.
