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
manager: craigg
ms.openlocfilehash: 268d5f00d787cef8dfdcb29bd9e091f81a5ed2c9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692171"
---
# <a name="catalog-functions"></a>카탈로그 함수
모든 데이터베이스에는 데이터베이스에 데이터를 저장 하는 방법에 대해 간략하게 설명 하는 구조체입니다. 예를 들어, 간단한 판매 주문 데이터베이스 테이블에 연결할 사용 되는 ID 열, 다음 그림에 표시 되는 구조가 있을 수 있습니다.  
  
 ![단순 데이터베이스 구조를 보여 줍니다](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 권한 같은 다른 정보와 함께이 구조는 데이터베이스 라는 시스템 테이블 집합에 저장 됩니다 *카탈로그* 라고도 되는 *데이터 사전*합니다.  
  
 응용 프로그램에 대 한 호출을 통해이 구조를 검색할 수는 *카탈로그 함수*합니다. 카탈로그 함수 결과 집합에는 정보를 통해 일반적으로 구현 반환 **선택** 카탈로그의 테이블에 대해 문의 합니다. 예를 들어 응용 프로그램은 시스템의 모든 테이블이나 특정 테이블의 모든 열에 대한 정보를 포함하는 결과 집합을 요청할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 데이터의 용도](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [ODBC의 카탈로그 함수](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
