---
title: CREATE TABLE 문을 NOT NULL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 5b1c2d2a96e12e09341d4bf34811bc7bcb6694e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910448"
---
# <a name="not-null-in-create-table-statements"></a>CREATE 테이블 문에서 NULL이 아님
일부 데이터베이스 및 특히 데스크톱 데이터베이스를 지원 하지 않습니다는 **NOT NULL** 열 제약 조건에서 **CREATE TABLE** 문. 자세한 내용은 참조 SQL_NON_NULLABLE_COLUMNS 옵션에는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.
