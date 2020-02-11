---
title: 카탈로그 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 232d2e9b7e9eb695a40058075ea511392e464a32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064405"
---
# <a name="catalog-functions"></a>카탈로그 함수
모든 데이터베이스에는 데이터를 데이터베이스에 저장 하는 방법을 간략하게 설명 하는 구조가 있습니다. 예를 들어 간단한 판매 주문 데이터베이스에는 다음 그림에 표시 된 구조가 있을 수 있습니다 .이 그림에서는 ID 열을 사용 하 여 테이블을 연결 합니다.  
  
 ![단순 데이터베이스 구조](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 권한 등의 다른 정보와 함께이 구조는 *데이터 사전이*라고도 하는 데이터베이스의 *카탈로그* 라는 시스템 테이블 집합에 저장 됩니다.  
  
 응용 프로그램은 *카탈로그 함수*를 호출 하 여이 구조를 검색할 수 있습니다. 카탈로그 함수는 결과 집합에 정보를 반환 하며 일반적으로 카탈로그의 테이블에 대해 **SELECT** 문을 통해 구현 됩니다. 예를 들어 애플리케이션은 시스템의 모든 테이블이나 특정 테이블의 모든 열에 대한 정보를 포함하는 결과 집합을 요청할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 데이터의 용도](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [ODBC의 카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
