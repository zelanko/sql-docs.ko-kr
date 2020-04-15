---
title: SQL 유형 식별자 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 95bf46844e9ed91aac1ec6cb93a298995f0901d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299773"
---
# <a name="sql-type-identifiers"></a>SQL 형식 식별자
각 데이터 원본은 자체 SQL 데이터 형식을 정의합니다. ODBC는 형식 식별자를 정의하고 각 형식 식별자에 매핑될 수 있는 SQL 데이터 형식의 일반적인 특성을 설명합니다. 기본 데이터 원본의 각 데이터 형식이 ODBC의 SQL 형식 식별자에 매핑되는 방식은 드라이버에 따라 다릅니다.  
  
 예를 들어 SQL_CHAR 일반적으로 1~254자 사이의 고정 길이를 가진 문자 열의 형식 식별자입니다. 이러한 특성은 많은 SQL 데이터 원본에 있는 CHAR 데이터 형식에 해당합니다. 따라서 응용 프로그램에서 열의 형식 식별자가 SQL_CHAR 것을 발견하면 CHAR 열을 다루고 있다고 가정할 수 있습니다. 그러나 열이 1에서 254자 사이라고 가정하기 전에 열의 바이트 길이를 확인해야 합니다. 예를 들어 SQL이 아닌 데이터 원본의 드라이버는 정확히 일치하지 않으므로 500자로 구성된 고정 길이 문자 열을 SQL_CHAR 또는 SQL_LONGVARCHAR 매핑할 수 있습니다.  
  
 ODBC는 다양한 SQL 형식 식별자를 정의합니다. 그러나 드라이버는 이러한 식별자를 모두 사용할 필요는 없습니다. 대신 기본 데이터 원본에서 지원하는 SQL 데이터 형식을 노출하는 데 필요한 식별자만 사용합니다. 기본 데이터 원본이 형식 식별자가 일치하지 않는 SQL 데이터 형식을 지원하는 경우 드라이버는 추가 형식 식별자를 정의할 수 있습니다. 자세한 내용은 [드라이버 관련 데이터 유형, 설명자 유형, 정보 유형, 진단 유형 및 특성을](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)참조하십시오.  
  
 SQL 형식 식별자에 대한 전체 설명은 부록 D: 데이터 [형식의 C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md) 참조하십시오.
