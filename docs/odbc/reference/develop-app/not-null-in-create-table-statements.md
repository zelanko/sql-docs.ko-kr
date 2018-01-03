---
title: "CREATE TABLE 문을 NOT NULL | Microsoft Docs"
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
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf0f66a1d3a5d1c7bb07ef90d25c61a99e7a7786
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="not-null-in-create-table-statements"></a>CREATE 테이블 문에서 NULL이 아님
일부 데이터베이스 및 특히 데스크톱 데이터베이스를 지원 하지 않습니다는 **NOT NULL** 열 제약 조건에서 **CREATE TABLE** 문. 자세한 내용은 참조 SQL_NON_NULLABLE_COLUMNS 옵션에는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.
