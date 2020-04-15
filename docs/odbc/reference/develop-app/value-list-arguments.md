---
title: 값 목록 인수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd655bd745c3bb06923e047d4134b286cf64703e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306744"
---
# <a name="value-list-arguments"></a>값 목록 인수
값 목록 인수는 일치에 사용할 쉼표로 구분된 값 목록으로 구성됩니다. ODBC 카탈로그 함수에는 **SQLTable의** *TableType* 인수라는 하나의 값 목록 인수만 있습니다. *tableType을* null 포인터로 설정하면 SQL_ALL_TABLE_TYPES 설정된 것과 동일하며, 이는 값 목록의 가능한 모든 멤버를 나열합니다. 이 인수는 SQL_ATTR_METADATA_ID 문 특성의 영향을 받지 않습니다. 자세한 내용은 [SQLTable](../../../odbc/reference/syntax/sqltables-function.md) 함수 설명을 참조하십시오.
