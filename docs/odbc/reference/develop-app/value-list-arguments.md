---
title: 목록 인수 값 | Microsoft Docs
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
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14c78f543f959e091e52db6881d49e4221667273
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="value-list-arguments"></a>인수 목록
값 목록 인수 목록이 일치 하는 데 사용할 쉼표로 구분 된 값으로 구성 됩니다. 인수가 하나의 값만 목록에는 ODBC 카탈로그 함수가:는 *TableType* 인수 **SQLTables**합니다. 설정 *TableType* null 포인터는 동일 SQL_ALL_TABLE_TYPES 값 목록의 가능한 모든 멤버를 열거 하는로 설정 하는 경우. 이 인수 SQL_ATTR_METADATA_ID 문 특성에 의해 영향을 받지 않습니다. 자세한 내용은 참조는 [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) 함수 설명 합니다.
