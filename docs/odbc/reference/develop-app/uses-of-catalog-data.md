---
title: 카탈로그 데이터 사용 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 429d42d4a82d0f9f34e33eb4f5f3293100505da9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306814"
---
# <a name="uses-of-catalog-data"></a>카탈로그 데이터의 용도
응용 프로그램은 다양한 방법으로 카탈로그 데이터를 사용합니다. 다음은 몇 가지 일반적인 용도입니다.  
  
-   **런타임에 SQL 문을 생성합니다.** 주문 입력 응용 프로그램과 같은 수직 응용 프로그램에는 하드 코딩된 SQL 문이 포함되어 있습니다. 응용 프로그램에서 사용하는 테이블과 열은 이러한 테이블에 액세스하는 명령문과 마찬가지로 미리 고정됩니다. 예를 들어 주문 입력 응용 프로그램에는 일반적으로 시스템에 새 주문을 추가하기 위한 매개 변수화된 단일 **INSERT** 문이 포함되어 있습니다.  
  
     ODBC를 사용하여 데이터를 검색하는 스프레드시트 프로그램과 같은 일반 응용 프로그램은 종종 사용자의 입력을 기반으로 런타임에 SQL 문을 생성합니다. 이러한 응용 프로그램은 사용자가 사용할 테이블 및 열의 이름을 입력해야 할 수 있습니다. 그러나 응용 프로그램에서 사용자가 선택할 수 있는 테이블 및 열 목록을 표시하는 경우 사용자에게 더 쉬울 수 있습니다. 이러한 목록을 작성하려면 응용 프로그램에서 **SQLTable** 및 SQLColumns 카탈로그 함수를 **호출합니다.**  
  
-   **개발 중 SQL 문을 생성합니다.** 응용 프로그램 개발 환경은 일반적으로 프로그래머가 프로그램을 개발하는 동안 데이터베이스 쿼리를 만들 수 있도록 합니다. 그런 다음 쿼리는 빌드 중인 응용 프로그램에서 하드 코딩됩니다.  
  
     이러한 환경에서는 **SQLTable** 및 **SQLColumns를** 사용하여 프로그래머가 선택할 수 있는 목록을 만들 수도 있습니다. 이러한 환경에서는 **SQLPrimaryKeys** 및 **SQLForeignKeys를** 사용하여 선택한 테이블 간의 관계를 자동으로 확인하고 표시하고 **SQLStatistics를** 사용하여 인덱싱된 필드를 결정하고 강조 표시하여 프로그래머가 효율적인 쿼리를 만들 수 있습니다.  
  
-   **커서 생성.** 스크롤 가능한 커서 엔진을 제공하는 응용 프로그램, 드라이버 또는 미들웨어는 **SQLSpecialColumns를** 사용하여 행을 고유하게 식별하는 열이나 열을 결정할 수 있습니다. 프로그램은 가져온 각 행에 대해 이러한 열의 값을 포함하는 *키 집합을* 빌드할 수 있습니다. 응용 프로그램이 행으로 다시 스크롤하면 이러한 값을 사용하여 행에 대한 최신 데이터를 가져옵니다. 스크롤 가능한 커서 및 키집합에 대한 자세한 내용은 [스크롤 가능한 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)를 참조하십시오.
