---
title: 카탈로그 데이터 사용 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9b75d59d8fc28e364f5826d95e7fc50cb6afda7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312529"
---
# <a name="uses-of-catalog-data"></a>카탈로그 데이터의 용도
응용 프로그램에서 다양 한 방법으로 카탈로그 데이터를 사용합니다. 몇 가지 일반적인 용도 다음과 같습니다.  
  
-   **런타임 시 SQL 문을 생성합니다.** 주문 입력 응용 프로그램 등의 수직 응용 프로그램 하드 코딩 된 SQL 문을 포함 합니다. 이러한 테이블에 액세스 하는 문을으로 테이블 및 열 응용 프로그램에서 사용 되는 런타임까지 고정 됩니다. 주문 입력 응용 프로그램 단일 일반적으로 포함 되는 예를 들어 매개 변수가 있는 **삽입** 시스템에 새 주문을 추가 하는 것에 대 한 문입니다.  
  
     ODBC를 사용 하 여 데이터를 검색 하는 스프레드시트 프로그램과 같은 일반 응용 프로그램 사용자 로부터 입력을 기반으로 런타임 시 SQL 문을 만들 수 있습니다. 이러한 응용 프로그램에 사용자 테이블 및 열을 사용 하 여 이름을 입력할 필요할 수 있습니다. 그러나는 것이 더 쉽습니다 사용자에 대 한 응용 프로그램이 테이블 및 사용자 선택 항목을 만들 수 있는 열 목록을 표시 합니다. 이러한 목록을 빌드하, 응용 프로그램 호출을 **SQLTables** 하 고 **SQLColumns** 카탈로그 함수입니다.  
  
-   **개발 하는 동안 SQL 문을 생성합니다.** 응용 프로그램 개발 환경에는 일반적으로 프로그램을 개발 하는 동안 데이터베이스 쿼리를 만들려면 프로그래머가 허용 합니다. 다음 쿼리는 작성 중인 응용 프로그램에 하드 코딩 합니다.  
  
     이러한 환경 사용할 수도 있습니다 **SQLTables** 하 고 **SQLColumns** 프로그래머가 선택 항목을 만들 수 있는 목록을 만듭니다. 이러한 환경도 사용할 수 있습니다 **SQLPrimaryKeys** 하 고 **SQLForeignKeys** 자동으로 결정 선택한 테이블 간의 관계를 표시 하 고 사용 하려면 **SQLStatistics** 를 확인 하 고 프로그래머는 효율적인 쿼리를 만들 수 있도록 인덱싱된 필드를 강조 표시 합니다.  
  
-   **커서를 생성합니다.** 응용 프로그램, 드라이버 또는 스크롤 가능 커서 엔진을 제공 하는 미들웨어를 사용할 수 있습니다 **SQLSpecialColumns** 는 열 또는 열을 행을 고유 하 게 식별을 확인 하려면. 프로그램을 빌드할 수는 *keyset* 를 가져온 각 행에 대 한 이러한 열의 값을 포함 하 합니다. 응용 프로그램을 행으로 다시 스크롤하면 하는 경우이 값을 사용 합니다 이러한 행에 대 한 최신 데이터를 인출할 수입니다. 스크롤 가능 커서 및 키 집합에 대 한 자세한 내용은 참조 하세요. [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)합니다.
