---
title: SQL_C_TCHAR | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42afb911dda26cbda53f9cd14c883abb3775b94b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270533"
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
SQL_C_TCHAR 형식 식별자는 데이터 형식을 실제로 식별 하지 않습니다. 유니코드 변환에 대 한 헤더 파일 내에 존재 하는 매크로 이며 유니코드의 설정에 따라 SQL_C_CHAR 또는 SQL_C_WCHAR 바뀝니다 **#define**합니다. ANSI 및 유니코드 응용 프로그램으로 컴파일되는 문자 데이터를 전송 하는 응용 프로그램에 두는 것이 유용 합니다.
