---
title: SQLDescribeCol 및 SQLColAttribute | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8bd21010908473e4216a02a504b2de25578d5c84
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299763"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 및 SQLColAttribute
**SQLDescribeCol** 및 **SQLColAttribute는** 결과 집합 메타데이터를 검색하는 데 사용됩니다. 이 두 함수의 차이점은 **SQLDescribeCol이** 항상 동일한 다섯 가지 정보(열 이름, 데이터 형식, 정밀도, 규모 및 nullability)를 반환하고 **SQLColAttribute는** 응용 프로그램에서 요청한 단일 정보를 반환한다는 것입니다. 그러나 **SQLColAttribute는** 열의 대/소문자 구분, 표시 크기, 업데이터 가능성 및 검색 가능성을 포함하여 훨씬 더 풍부한 메타데이터를 반환할 수 있습니다.  
  
 많은 응용 프로그램, 특히 데이터만 표시하는 응용 프로그램에는 **SQLDescribeCol**에서 반환되는 메타데이터만 필요합니다. 이러한 응용 프로그램의 경우 정보가 단일 호출에서 반환되므로 **SQLDescribeCol을** **SQLColAttribute보다** 사용하는 것이 더 빠릅니다. 다른 응용 프로그램, 특히 데이터를 업데이트하는 응용 프로그램에는 **SQLColAttribute에서** 반환되는 추가 메타데이터가 필요하므로 두 함수를 모두 사용합니다. 또한 **SQLColAttribute는** 드라이버 별 메타데이터를 지원합니다. 자세한 내용은 [드라이버 관련 데이터 유형, 설명자 유형, 정보 유형, 진단 유형 및 특성을](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)참조하십시오.  
  
 응용 프로그램은 명령문이 준비되거나 실행된 후 결과 집합에 대한 커서가 닫히기 전에 언제든지 결과 집합 메타데이터를 검색할 수 있습니다. 명령문이 준비되고 실행되기 전에 결과 집합 메타데이터가 필요한 응용 프로그램은 거의 없습니다. 가능하면 일부 데이터 원본이 준비된 문에 대한 메타데이터를 반환할 수 없고 드라이버에서 이 기능을 에뮬레이션하는 것이 느린 프로세스이기 때문에 응용 프로그램은 문이 실행될 때까지 메타데이터를 검색할 때까지 기다려야 합니다. 예를 들어 드라이버는 **SELECT** 문의 **WHERE** 절을 **WHERE 1 = 2** 절로 대체하고 결과 문을 실행하여 0행 결과 집합을 생성할 수 있습니다.  
  
 메타데이터는 데이터 원본에서 검색하는 데 비용이 많이 드는 경우가 많습니다. 따라서 드라이버는 서버에서 검색한 모든 메타데이터를 캐시하고 결과 집합의 커서가 열려 있는 동안 보관해야 합니다. 또한 응용 프로그램은 절대적으로 필요한 메타데이터만 요청해야 합니다.
