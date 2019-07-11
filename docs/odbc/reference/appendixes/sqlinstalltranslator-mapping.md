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
ms.openlocfilehash: 50bfa00f482110d3d0695ef249e8758b5db02c80
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792808"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 매핑
때 ODBC *2.x* 응용 프로그램 호출 **SQLInstallTranslator** ODBC를 통해 *3.x* 드라이버를 드라이버 관리자에 대 한 호출 매핑합니다  **SQLInstallTranslatorEx**합니다. 응용 프로그램을 호출 하지 않아야 **SQLInstallTranslator** odbc에서 *3.x* 사용 하 여 드라이버 관리자는 *lpszInfFile* 인수는 NULL이 아닌 값으로 설정 합니다. ODBC입니다. ODBC에서 사용 되는 INF 파일 *2.x* ODBC에서 더 이상 지원 되지 *3.x*이전 버전과 호환성을 위해서도 합니다.
