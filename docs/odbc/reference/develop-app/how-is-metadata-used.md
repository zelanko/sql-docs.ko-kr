---
title: 메타데이터는 어떻게 사용되나요? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3604e9f3bd47a10ae1a6e5ec401b198675c2d3e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149295"
---
# <a name="how-is-metadata-used"></a>메타데이터는 어떻게 사용되나요?
응용 프로그램에서는 대부분의 결과 집합 작업에 대해 메타데이터를 요구합니다. 예를 들어 응용 프로그램에서는 열의 데이터 형식을 사용하여 해당 열에 바인딩할 변수의 종류를 확인하고 문자 열의 바이트 길이 사용 하 여 해당 열에서 데이터를 표시 해야 하는 공간 크기를 확인 합니다. 응용 프로그램에서 열의 메타데이터를 확인하는 방법은 응용 프로그램 종류에 따라 다릅니다.  
  
 수직 응용 프로그램을 미리 정의 된 테이블 작업 및 해당 테이블에서 미리 정의 된 작업을 수행 합니다. 응용 프로그램을 작성 하 고 응용 프로그램 개발자에 의해 제어 됩니다 하기 전에 이러한 응용 프로그램에 대 한 결과 집합 메타 데이터 정의 때문에 응용 프로그램에 하드 코딩 수 있습니다. 예를 들어 주문 ID 열이 데이터 원본에 4바이트 정수로 정의된 경우 응용 프로그램에서는 항상 해당 열에 4바이트 정수를 바인딩할 수 있습니다. 메타데이터가 응용 프로그램에 하드 코딩되면 응용 프로그램에서 사용하는 테이블의 변경은 일반적으로 응용 프로그램 코드의 변경을 암시합니다. 이러한 변경 내용은 항상 응용 프로그램의 새 릴리스의 일부로 때문에 문제가 거의입니다.  
  
 수직 응용 프로그램과 마찬가지로 사용자 지정 응용 프로그램은 일반적으로 미리 정의 된 테이블을 사용 하 고 해당 테이블에 대 한 미리 정의 된 작업을 수행 합니다. 예를 들어, 응용 프로그램 기록 될 수 있습니다; 그리고 세 가지 다른 데이터 원본 간에 데이터를 전송 일반적으로 응용 프로그램을 작성 하는 경우 데이터를 전송 이라고 합니다. 따라서 사용자 지정 응용 프로그램 하드 코드 된 메타 데이터가 있어야 하는 경향이 있습니다.  
  
 일반 응용 프로그램, 특히는 임시 쿼리를 지 원하는, 만든 결과 집합의 메타 데이터를 미리 알 거의 없습니다. 따라서 이러한 함수를 사용 하 여 런타임에 메타 데이터를 검색 해야 **SQLNumResultCols**를 **SQLDescribeCol**, 및 **SQLColAttribute**에 설명 되어 있는 다음 섹션인 [SQLDescribeCol 및 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)합니다.  
  
 해당 형식에 관계 없이 모든 응용 프로그램 카탈로그 함수에서 반환한 결과 집합에 대 한 메타 데이터를 하드 코딩할 수 있습니다. 이러한 결과 집합은이 설명서의 참조 섹션에 정의 됩니다.
