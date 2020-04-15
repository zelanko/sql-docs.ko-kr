---
title: 카탈로그 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb28ec6f4ea299dae8737fc707fd53e4d102442d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305204"
---
# <a name="catalog-functions"></a>카탈로그 함수
모든 데이터베이스에는 데이터가 데이터베이스에 저장되는 방법을 설명하는 구조가 있습니다. 예를 들어 간단한 판매 주문 데이터베이스에는 ID 열을 사용하여 테이블을 연결하는 다음 그림에 표시된 구조가 있을 수 있습니다.  
  
 ![단순 데이터베이스 구조](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 이 구조는 권한과 같은 다른 정보와 함께 데이터베이스 *카탈로그라고* 하는 시스템 테이블 집합에 저장되며, 이 테이블은 *데이터 사전이라고도*합니다.  
  
 응용 프로그램은 *카탈로그 함수에*대한 호출을 통해 이 구조를 검색할 수 있습니다. 카탈로그 함수는 결과 집합에서 정보를 반환하며 일반적으로 카탈로그의 테이블에 대해 **SELECT** 문을 통해 구현됩니다. 예를 들어 애플리케이션은 시스템의 모든 테이블이나 특정 테이블의 모든 열에 대한 정보를 포함하는 결과 집합을 요청할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 데이터의 용도](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [ODBC의 카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
