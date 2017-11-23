---
title: "카탈로그 데이터의 사용 | Microsoft Docs"
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
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c77be1b431a7f7e2cf8c040df7ceb9a9feaf321a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="uses-of-catalog-data"></a>카탈로그 데이터의 용도
응용 프로그램 카탈로그 데이터는 여러 가지 방법으로 사용합니다. 몇 가지 일반적인 용도 다음과 같습니다.  
  
-   **런타임 시 SQL 문을 구성 합니다.** 주문 입력 응용 프로그램 등의 수직 응용 프로그램에는 하드 코드 된 SQL 문을 포함 합니다. 테이블 및 응용 프로그램에서 사용 되는 열은 이러한 테이블에 액세스 하는 문을 미리 고정 됩니다. 일반적으로 포함 되어는 단일을 예를 들어 주문 입력 응용 프로그램 매개 변수가 있는 **삽입** 새 주문 시스템에 추가 하는 데 문입니다.  
  
     종종 ODBC를 사용 하 여 데이터를 검색 하는 스프레드시트 프로그램 등의 일반 응용 프로그램 사용자의 입력에 따라 실행 시 SQL 문을 생성 합니다. 이러한 응용 프로그램에 사용자를 사용 하는 열과 테이블의 이름을 입력할 수 필요 합니다. 그러나 됩니다 사용자가 보다 쉽게 응용 프로그램이 테이블 및 사용자 선택 항목을 만들 수 있는 열 목록에 표시 합니다. 이러한 목록을 만들려는 응용 프로그램 호출에서 **SQLTables** 및 **SQLColumns** 카탈로그 함수입니다.  
  
-   **개발 하는 동안 SQL 문을 구성 합니다.** 일반적으로 응용 프로그램 개발 환경을 사용 하는 프로그램을 개발 하는 동안 데이터베이스 쿼리를 만들 수 있습니다. 다음 쿼리는 작성 중인 응용 프로그램에 하드 코드 됩니다.  
  
     이러한 환경도 사용할 수 **SQLTables** 및 **SQLColumns** 프로그래머는 선택 항목을 만들 수 있는 목록을 만듭니다. 이러한 환경도 사용할 수 있습니다 **SQLPrimaryKeys** 및 **SQLForeignKeys** 자동으로 결정 하 고 선택한 테이블 간의 관계를 표시 및 사용 하 여 **SQLStatistics** 확인 하 고 프로그래머가 효율적인 쿼리를 만들 수 있도록 인덱싱된 필드를 강조 표시 합니다.  
  
-   **커서를 생성 하는입니다.** 응용 프로그램, 드라이버, 또는 스크롤할 수 있는 커서 엔진을 제공 하는 미들웨어 악용 **SQLSpecialColumns** 결정 열 또는 열에는 행을 고유 하 게 식별 하 합니다. 프로그램을 작성할 수는 *키 집합* 인출 된 각 행에 대해 이러한 열의 값이 들어 있는입니다. 응용 프로그램을 행으로 다시 스크롤하면 이러한 값을 행에 대 한 가장 최근 데이터를 인출 유도할 합니다. 스크롤 가능 커서와 키 집합에 대 한 자세한 내용은 참조 [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)합니다.
