---
title: 메타 데이터 사용은 어떻게 합니까? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c4779c5e60b97a389ebf686678c9a989fb933cb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910798"
---
# <a name="how-is-metadata-used"></a>메타 데이터 사용은 어떻게 합니까?
응용 프로그램에서는 대부분의 결과 집합 작업에 대해 메타데이터를 요구합니다. 예를 들어 응용 프로그램에서는 열의 데이터 형식을 사용하여 해당 열에 바인딩할 변수의 종류를 확인하고 문자 열의 바이트 길이 사용 하 여 해당 열의 데이터를 표시 하는 데 필요한 공간의 크기를 결정 합니다. 응용 프로그램에서 열의 메타데이터를 확인하는 방법은 응용 프로그램 종류에 따라 다릅니다.  
  
 수직 응용 프로그램을 미리 정의 된 테이블 작업을 하 고 해당 테이블에 대 한 미리 정의 된 작업을 수행 합니다. 이러한 응용 프로그램에 대 한 결과 집합 메타 데이터는 응용 프로그램을 작성 하 고 응용 프로그램 개발자에 의해 제어를 정의 되므로 응용 프로그램에 하드 코딩 수 있습니다. 예를 들어 주문 ID 열이 데이터 원본에 4바이트 정수로 정의된 경우 응용 프로그램에서는 항상 해당 열에 4바이트 정수를 바인딩할 수 있습니다. 메타데이터가 응용 프로그램에 하드 코딩되면 응용 프로그램에서 사용하는 테이블의 변경은 일반적으로 응용 프로그램 코드의 변경을 암시합니다. 이러한 변경 내용은 항상 응용 프로그램의 새 릴리스의 일부로 서 때문에 문제를 거의입니다.  
  
 세로 응용 프로그램과 마찬가지로 사용자 지정 응용 프로그램은 일반적으로 미리 정의 된 테이블을 사용 하 고 해당 테이블에서 미리 정의 된 작업을 수행 합니다. 예를 들어 세 개의 서로 다른 데이터 원본 간에 데이터를 전송할 응용 프로그램를 작성 될 수도 일반적으로 응용 프로그램 기록 될 때 데이터를 전송 알려져 있습니다. 따라서 사용자 지정 응용 프로그램 하드 코드 된 메타 데이터를 가져야 하는 경향이 있습니다.  
  
 특히 임시 쿼리를 지 원하는, 거의 만든 결과 집합의 메타 데이터를 파악 하는 일반 응용 프로그램입니다. 따라서 런타임에 함수를 사용 하 여 메타 데이터를 검색 해야은 **SQLNumResultCols**, **SQLDescribeCol**, 및 **SQLColAttribute**에 다음 섹션, [SQLDescribeCol 및 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)합니다.  
  
 형식에 관계 없이 모든 응용 프로그램 카탈로그 함수에서 반환 된 결과 집합에 대 한 하드 코딩 메타 데이터를 수 있습니다. 이러한 결과 집합은이 설명서의 참조 섹션에 정의 됩니다.
