---
title: 카탈로그 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9f6b9990799027270c913cb332ce5a0ffc71171
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="catalog-functions"></a>카탈로그 함수
모든 데이터베이스는 데이터베이스에 데이터가 저장 되는 요약 된 구조가 있습니다. 예를 들어 판매 주문 간단한 데이터베이스에는 ID 열을 사용 하 여 테이블을 연결를 다음 그림에 표시 되는 구조는 있습니다.  
  
 ![단순 데이터베이스 구조를 보여 줍니다](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 권한 같은 다른 정보와 함께이 구조는 데이터베이스 라는 시스템 테이블 집합에 저장 됩니다 *카탈로그* 는 라고도 *데이터 사전*합니다.  
  
 응용 프로그램에 대 한 호출을 통해이 구조를 검색할 수는 *카탈로그 함수*합니다. 카탈로그 함수 반환 되며 결과 집합의 정보를 통해 일반적으로 구현 **선택** 카탈로그의 테이블에 대해 문을 합니다. 예를 들어 응용 프로그램은 시스템의 모든 테이블이나 특정 테이블의 모든 열에 대한 정보를 포함하는 결과 집합을 요청할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 데이터의 용도](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [ODBC의 카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
