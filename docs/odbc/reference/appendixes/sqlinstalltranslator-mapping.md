---
title: "SQLInstallTranslator 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 07308a2c737f2fbe6857d8a65a913f881b8e658f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 매핑
경우는 ODBC 2. *x* 응용 프로그램 호출 **SQLInstallTranslator** ODBC 3*.x* 드라이버를 드라이버 관리자에 대 한 호출 매핑합니다 **SQLInstallTranslatorEx**. 응용 프로그램을 호출 하지 않아야 **SQLInstallTranslator** ODBC 3에서*.x* 와 드라이버 관리자는 *lpszInfFile* 인수는 NULL이 아닌 값으로 설정 합니다. ODBC 합니다. ODBC 2에서 사용 되는 INF 파일입니다. *x* ODBC 3에서 더 이상 지원*.x*이전 버전과 호환성에 대 한도입니다.

