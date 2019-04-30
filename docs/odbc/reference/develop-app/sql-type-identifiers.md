---
title: SQL 유형 식별자 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1763ee0cd8c5bc2017160de44b9c047781649eba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150026"
---
# <a name="sql-type-identifiers"></a>SQL 형식 식별자
각 데이터 원본에는 자체 SQL 데이터 형식을 정의합니다. ODBC 형식 식별자를 정의 하 고 각 형식 식별자에 매핑될 수 있는 SQL 데이터 형식의 일반 특징을 설명 합니다. 드라이버 관련 ODBC SQL 형식 식별자에 내부 데이터 소스의 각 데이터 유형에 매핑되는 방법을 것입니다.  
  
 예를 들어, SQL_CHAR, 일반적으로 1 ~ 254 자 사이의 고정된 길이 문자 열에 대 한 형식 식별자입니다. 이러한 특징 많은 SQL 데이터 원본에 CHAR 데이터 형식에 해당 합니다. 따라서 응용 프로그램 SQL_CHAR 열에 대 한 형식 식별자는 데이터를 검색 하는 경우 아마도 처리 하는 CHAR 열 가정할 수 있습니다. 그러나 여전히 확인 해야 해당 가정 하기 전에 열의 바이트 길이가 1 ~ 254 자; 둘 다 있으므로 비 SQL 데이터 원본의 경우 예를 들어 드라이버 SQL_CHAR 또는 SQL_LONGVARCHAR에 500 문자의 고정 길이 문자 열 매핑할 수 있습니다 정확 하 게 일치 합니다.  
  
 ODBC는 SQL 유형 식별자의 다양 한을 정의합니다. 그러나 드라이버는 이러한 식별자의 모든 사용할 필요가 없습니다. 대신, 기본 데이터 원본에서 지 원하는 SQL 데이터 형식을 노출 해야 하는 식별자에만 사용 합니다. 데이터 원본에서 SQL 데이터 형식을 지 원하는 경우 해당 하는 식별자가 없는 형식, 드라이버는 추가 형식 식별자를 정의할 수 있습니다. 자세한 내용은 [드라이버별 데이터 형식, 설명자 유형, 정보 유형, 진단 유형 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)합니다.  
  
 에 대 한 전체 설명은 SQL 유형 식별자를 참조 하세요 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 부록 d: 데이터 형식입니다.
