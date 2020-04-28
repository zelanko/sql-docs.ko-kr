---
title: SQL 형식 식별자 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299773"
---
# <a name="sql-type-identifiers"></a>SQL 형식 식별자
각 데이터 원본은 자체 SQL 데이터 형식을 정의 합니다. ODBC는 형식 식별자를 정의 하 고 각 형식 식별자에 매핑될 수 있는 SQL 데이터 형식의 일반 특성을 설명 합니다. 기본 데이터 원본의 각 데이터 형식이 ODBC의 SQL 형식 식별자에 매핑되는 방식에 대 한 드라이버 관련 방법입니다.  
  
 예를 들어 SQL_CHAR는 고정 길이를 가진 문자 열에 대 한 형식 식별자 이며 일반적으로 1에서 254 자 사이입니다. 이러한 특징은 많은 SQL 데이터 원본에 있는 CHAR 데이터 형식에 해당 합니다. 따라서 응용 프로그램에서 열의 형식 식별자가 SQL_CHAR 되는 것으로 검색 되는 경우 CHAR 열을 처리 하는 것으로 간주할 수 있습니다. 그러나 열의 바이트 길이는 1 ~ 007e; 254 자 여야 한다고 가정 하 고 확인 해야 합니다. 예를 들어 SQL 이외의 데이터 원본에 대 한 드라이버는 500 문자의 고정 길이 문자 열을 SQL_CHAR 또는 SQL_LONGVARCHAR에 매핑할 수 있습니다 .이는 정확히 일치 하지 않기 때문입니다.  
  
 ODBC는 다양 한 SQL 형식 식별자를 정의 합니다. 그러나 드라이버에서 이러한 식별자를 모두 사용할 필요는 없습니다. 대신 기본 데이터 원본에서 지원 되는 SQL 데이터 형식을 노출 하는 데 필요한 식별자만 사용 합니다. 기본 데이터 원본에서 형식 식별자가 일치 하지 않는 SQL 데이터 형식을 지 원하는 경우 드라이버에서 추가 형식 식별자를 정의할 수 있습니다. 자세한 내용은 [드라이버별 데이터 형식, 설명자 형식, 정보 형식, 진단 유형 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)을 참조 하세요.  
  
 SQL 형식 식별자에 대 한 자세한 설명은 부록 D: 데이터 형식의 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 을 참조 하세요.
