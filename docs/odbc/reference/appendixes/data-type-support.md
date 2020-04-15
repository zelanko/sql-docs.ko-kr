---
title: 데이터 유형 지원 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abfe85ee32fb9ff4a8499c9949c0685563fec70
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284430"
---
# <a name="data-type-support"></a>데이터 형식 지원
ODBC 드라이버는 SQL_CHAR 중 하나 이상을 지원하고 SQL_VARCHAR. 다른 데이터 형식에 대한 지원은 드라이버 또는 데이터 원본의 SQL-92 준수 수준에 따라 결정됩니다. 응용 프로그램은 **SQLGetTypeInfo를** 호출하여 드라이버에서 지원하는 데이터 형식을 결정해야 합니다.  
  
 데이터 유형에 대한 자세한 내용은 [부록 D: 데이터 유형을](../../../odbc/reference/appendixes/appendix-d-data-types.md)참조하십시오.
