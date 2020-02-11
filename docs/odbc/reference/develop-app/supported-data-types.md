---
title: 지원 되는 데이터 형식 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f5ec0f3943fd52540f094a23e9b3f9f3886e1371
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114082"
---
# <a name="supported-data-types"></a>지원되는 데이터 형식
Dbms에서 지 원하는 데이터 형식은 매우 다양 합니다. 응용 프로그램은 **SQLGetTypeInfo**를 호출 하 여 지원 되는 데이터 형식의 이름과 특성을 결정할 수 있습니다. 데이터 형식 이름의 넓은 변동 때문에 응용 프로그램은 **CREATE TABLE** 문에서 **SQLGetTypeInfo** 에 의해 반환 되는 데이터 형식 이름을 사용 해야 합니다. 자세한 내용은 [ODBC의 데이터 형식](../../../odbc/reference/develop-app/data-types-in-odbc.md)을 참조 하세요.
