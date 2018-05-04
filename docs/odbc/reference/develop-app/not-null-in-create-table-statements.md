---
title: CREATE TABLE 문을 NOT NULL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63e2ed384033370b91a8321ad9c6165b72570f72
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="not-null-in-create-table-statements"></a>CREATE 테이블 문에서 NULL이 아님
일부 데이터베이스 및 특히 데스크톱 데이터베이스를 지원 하지 않습니다는 **NOT NULL** 열 제약 조건에서 **CREATE TABLE** 문. 자세한 내용은 참조 SQL_NON_NULLABLE_COLUMNS 옵션에는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.
