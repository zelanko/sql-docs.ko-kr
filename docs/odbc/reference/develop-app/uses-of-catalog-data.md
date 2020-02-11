---
title: 카탈로그 데이터의 사용 | Microsoft Docs
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
ms.openlocfilehash: dc8999c0a7189772145f553646b45eb1f1fbd695
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091610"
---
# <a name="uses-of-catalog-data"></a>카탈로그 데이터의 용도
응용 프로그램은 다양 한 방법으로 카탈로그 데이터를 사용 합니다. 몇 가지 일반적인 용도는 다음과 같습니다.  
  
-   **런타임에 SQL 문 생성** 주문 입력 응용 프로그램과 같은 수직 응용 프로그램에는 하드 코드 된 SQL 문이 포함 되어 있습니다. 응용 프로그램에서 사용 하는 테이블 및 열은 이러한 테이블에 액세스 하는 문과 마찬가지로 미리 고정 되어 있습니다. 예를 들어 주문 입력 응용 프로그램에는 일반적으로 시스템에 새 주문을 추가 하기 위한 매개 변수가 있는 단일 **INSERT** 문이 포함 되어 있습니다.  
  
     ODBC를 사용 하 여 데이터를 검색 하는 스프레드시트 프로그램과 같은 일반 응용 프로그램은 종종 사용자의 입력을 기반으로 런타임 시 SQL 문을 생성 합니다. 이러한 응용 프로그램을 사용 하려면 사용자가 테이블 및 열 이름을 입력 해야 합니다. 그러나 응용 프로그램에 사용자가 선택할 수 있는 테이블 및 열 목록이 표시 되는 경우 사용자에 게 더 쉽게 사용할 수 있습니다. 이러한 목록을 빌드하기 위해 응용 프로그램은 **Sqltables** 및 **sqltables** 카탈로그 함수를 호출 합니다.  
  
-   **개발 중에 SQL 문 생성** 일반적으로 응용 프로그램 개발 환경에서는 프로그래머가 프로그램을 개발 하는 동안 데이터베이스 쿼리를 만들 수 있습니다. 그러면 작성 중인 응용 프로그램에서 쿼리가 하드 코딩 됩니다.  
  
     이러한 환경에서는 **Sqltables** 및 **sqltables** 를 사용 하 여 프로그래머가 선택할 수 있는 목록을 만들 수도 있습니다. 이러한 환경에서는 **Sqlprimarykeys** 및 **SQLForeignKeys** 를 사용 하 여 선택한 테이블 간의 관계를 자동으로 결정 하 고 표시할 수 있으며, **SQLStatistics** 를 사용 하 여 인덱싱된 필드를 확인 하 고 강조 표시할 수도 있습니다. 그러면 프로그래머가 효율적인 쿼리를 만들 수  
  
-   **커서 생성** 스크롤할 수 있는 커서 엔진을 제공 하는 응용 프로그램, 드라이버 또는 미들웨어는 **SQLSpecialColumns** 을 사용 하 여 행을 고유 하 게 식별 하는 열을 확인할 수 있습니다. 이 프로그램은 인출 된 각 행에 대해 이러한 열의 값을 포함 하는 *키 집합* 을 작성할 수 있습니다. 응용 프로그램은 다시 행으로 스크롤할 때 이러한 값을 사용 하 여 행에 대 한 최신 데이터를 가져옵니다. 스크롤 가능 커서 및 키 집합이 비동기적에 대 한 자세한 내용은 [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)를 참조 하세요.
