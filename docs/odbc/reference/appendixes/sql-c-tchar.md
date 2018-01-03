---
title: SQL_C_TCHAR | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 63c23a242b7acd7dd3cf10acb3f60dea980cd398
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
실제로 SQL_C_TCHAR 형식 식별자는 데이터 형식을 나타내지 않습니다. 유니코드 변환에 대 한 헤더 파일 내에 존재 하는 매크로 이며 유니코드의 설정에 따라 SQL_C_CHAR 또는 SQL_C_WCHAR로 교체 되는지 **#define**합니다. ANSI 및 유니코드 응용 프로그램으로 컴파일되는 문자 데이터를 전송 하는 응용 프로그램에 것이 유용 합니다.
