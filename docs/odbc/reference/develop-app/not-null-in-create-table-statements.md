---
title: CREATE TABLE 문의 NOT NULL입니다. | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 808cddbd805db09d1b5c356d5b5af5734a5dcc16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086324"
---
# <a name="not-null-in-create-table-statements"></a>CREATE TABLE 문의 NOT NULL
일부 데이터베이스 및 특히 데스크톱 데이터베이스는 **CREATE TABLE** 문에서 **not NULL** 열 제약 조건을 지원 하지 않습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명의 SQL_NON_NULLABLE_COLUMNS 옵션을 참조 하십시오.
