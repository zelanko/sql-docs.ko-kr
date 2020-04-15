---
title: 지원되는 데이터 유형 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d19cde2d531819a60229dd7a780181571e169503
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307784"
---
# <a name="supported-data-types"></a>지원되는 데이터 형식
DBMS에서 지원하는 데이터 형식은 상당히 다양합니다. 응용 프로그램은 **SQLGetTypeInfo**를 호출하여 지원되는 데이터 형식의 이름과 특성을 확인할 수 있습니다. 데이터 형식 이름의 다양한 변형으로 인해 응용 프로그램은 **CREATE TABLE** 문에서 **SQLGetTypeInfo에서** 반환된 데이터 형식 이름을 사용해야 합니다. 자세한 내용은 [ODBC의 데이터 형식을](../../../odbc/reference/develop-app/data-types-in-odbc.md)참조하십시오.
