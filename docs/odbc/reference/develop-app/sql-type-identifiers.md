---
title: "SQL 유형 식별자 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d0565ddfffb5b74344aaa41a1d0dfd243c590850
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sql-type-identifiers"></a>SQL 유형 식별자
각 데이터 원본 자체 SQL 데이터 형식을 정의합니다. ODBC 형식 식별자를 정의 하 고 각 형식 식별자에 매핑될 수 있는 SQL 데이터 형식의 일반적인 특성을 설명 합니다. 드라이버 관련 odbc SQL 형식 식별자에 매핑되는 데이터 원본에서 각 데이터 형식 방법을 이며합니다  
  
 예를 들어 SQL_CHAR은 일반적으로 1-254 자 사이의 고정 길이 문자 열에 대 한 형식 식별자입니다. 이러한 특성은 여러 SQL 데이터 원본에 CHAR 데이터 형식에 해당 합니다. 따라서 열에 대 한 유형 식별자 SQL_CHAR 임을 확인 하는 응용 프로그램 때 것을 처리 하는 CHAR 열이 있는 가정할 수 있습니다. 그러나 여전히 확인 해야 있다는 가정 하기 전에 열의 바이트 길이 1-254 자입니다. 둘 다 때문에 비 SQL 데이터 원본의 경우 예를 들어 드라이버 SQL_CHAR 또는 SQL_LONGVARCHAR에 고정 길이 문자 열 500 자 매핑될 수 있습니다 정확 하 게 일치 합니다.  
  
 ODBC는 SQL 유형 식별자의 다양 한를 정의합니다. 그러나, 드라이버는 이러한 식별자의 모든 사용 필요가 없습니다. 대신, 기본 데이터 원본에서 지 원하는 SQL 데이터 형식을 노출 하는 데 필요한 식별자만 사용 합니다. 데이터 원본에 SQL 데이터 형식을 지 원하는 경우 유형 식별자 없이 해당, 드라이버 추가 형식 식별자를 정의할 수 있습니다. 자세한 내용은 참조 [드라이버 관련 데이터 형식, 형식 설명자, 정보 유형, 진단 형식 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)합니다.  
  
 에 대 한 전체 설명은 SQL 유형 식별자를 참조 하세요. [C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md) 부록 d: 데이터 형식에서입니다.
