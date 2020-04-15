---
title: 메타데이터는 어떻게 사용되나요? | Microsoft 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbbba96fa2e99a2ccc0618f31e3b29e7d479f703
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300173"
---
# <a name="how-is-metadata-used"></a>메타데이터는 어떻게 사용되나요?
애플리케이션에서는 대부분의 결과 집합 작업에 대해 메타데이터를 요구합니다. 예를 들어 애플리케이션에서는 열의 데이터 형식을 사용하여 해당 열에 바인딩할 변수의 종류를 확인하고 문자 열의 바이트 길이를 사용하여 해당 열의 데이터를 표시하는 데 필요한 공간을 결정합니다. 애플리케이션에서 열의 메타데이터를 확인하는 방법은 애플리케이션 종류에 따라 다릅니다.  
  
 수직 응용 프로그램은 미리 정의된 테이블로 작동하며 해당 테이블에서 미리 정의된 작업을 수행합니다. 이러한 응용 프로그램에 대한 결과 집합 메타데이터는 응용 프로그램을 작성하기 전에 정의되고 응용 프로그램 개발자가 제어하므로 응용 프로그램에 하드 코딩할 수 있습니다. 예를 들어 주문 ID 열이 데이터 원본에 4바이트 정수로 정의된 경우 애플리케이션에서는 항상 해당 열에 4바이트 정수를 바인딩할 수 있습니다. 메타데이터가 애플리케이션에 하드 코딩되면 애플리케이션에서 사용하는 테이블의 변경은 일반적으로 애플리케이션 코드의 변경을 암시합니다. 이러한 변경은 일반적으로 응용 프로그램의 새 릴리스의 일부로 이루어지기 때문에 이 문제는 거의 문제가 되지 않습니다.  
  
 수직 응용 프로그램과 마찬가지로 사용자 지정 응용 프로그램은 일반적으로 미리 정의된 테이블로 작동하며 해당 테이블에서 미리 정의된 작업을 수행합니다. 예를 들어, 세 가지 서로 다른 데이터 원본 간에 데이터를 전송하기 위해 응용 프로그램을 작성할 수 있습니다. 전송할 데이터는 일반적으로 응용 프로그램을 작성할 때 알 수 있습니다. 따라서 사용자 지정 응용 프로그램에는 하드 코딩된 메타데이터도 있는 경향이 있습니다.  
  
 일반 응용 프로그램, 특히 임시 쿼리를 지원하는 응용 프로그램은 만든 결과 집합의 메타데이터를 거의 알지 않습니다. 따라서 다음 섹션인 **SQLDescribeCol** [SQLDescribeCol 및 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)함수를 사용하여 런타임에 **SQLColAttribute**메타데이터를 검색해야 합니다. **SQLNumResultCols**  
  
 유형에 관계없이 모든 응용 프로그램은 카탈로그 함수에서 반환되는 결과 집합에 대한 메타데이터를 하드코딩할 수 있습니다. 이러한 결과 집합은 이 설명서의 참조 섹션에 정의되어 있습니다.
