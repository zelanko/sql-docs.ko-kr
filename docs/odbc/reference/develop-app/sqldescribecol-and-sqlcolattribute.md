---
title: SQLDescribeCol 및 SQLColAttribute | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d602368475c6f1326cc615453116e898b1c1892f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107439"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 및 SQLColAttribute
**SQLDescribeCol** 및 **sqlcolattribute** 는 결과 집합 메타 데이터를 검색 하는 데 사용 됩니다. 이러한 두 함수 간의 차이점은 **SQLDescribeCol** 는 항상 동일한 5 가지 정보 (열 이름, 데이터 형식, 전체 자릿수, 소수 자릿수 및 null 허용 여부)를 반환 하는 반면 **sqlcolattribute** 는 응용 프로그램에서 요청 하는 단일 정보를 반환 한다는 것입니다. 그러나 **Sqlcolattribute** 는 열에서 대/소문자 구분, 표시 크기, 업데이트 가능성 및 높이려는을 포함 하 여 훨씬 더 다양 한 메타 데이터를 반환할 수 있습니다.  
  
 특히 데이터만 표시 하는 많은 응용 프로그램에는 **SQLDescribeCol**에서 반환 되는 메타 데이터만 필요 합니다. 이러한 응용 프로그램의 경우 정보는 단일 호출로 반환 되므로 **Sqlcolattribute** 보다 **SQLDescribeCol** 를 사용 하는 것이 더 빠릅니다. 특히 데이터를 업데이트 하는 다른 응용 프로그램의 경우 **Sqlcolattribute** 에서 반환 하는 추가 메타 데이터가 필요 하므로 두 함수를 모두 사용 합니다. 또한 **Sqlcolattribute** 는 드라이버별 메타 데이터를 지원 합니다. 자세한 내용은 [드라이버별 데이터 형식, 설명자 형식, 정보 형식, 진단 유형 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)을 참조 하세요.  
  
 응용 프로그램은 문이 준비 되거나 실행 된 후에 언제 든 지 결과 집합 메타 데이터를 검색 하 고, 결과 집합 위에 커서를 닫을 수 있습니다. 문을 준비 하 고 실행 하기 전에 응용 프로그램에는 결과 집합 메타 데이터가 필요 합니다. 가능 하면 응용 프로그램은 문을 실행할 때까지 메타 데이터를 검색 하기 위해 대기 해야 합니다. 일부 데이터 소스는 준비 된 문에 대 한 메타 데이터를 반환할 수 없고 드라이버에서이 기능을 에뮬레이트하는 경우가 종종 있습니다. 예를 들어 **SELECT** 문의 where 절을 **1 = 2** 로 바꾸고 결과 문을 실행 하 여 드라이버에서 행이 **없는** 결과 집합을 생성할 수 있습니다.  
  
 메타 데이터는 데이터 원본에서 검색 하는 데 비용이 많이 듭니다. 따라서 드라이버는 서버에서 검색 하는 모든 메타 데이터를 캐시 하 고 결과 집합 위에 커서가 열려 있는 동안에는이를 보관 해야 합니다. 또한 응용 프로그램은 정말로 필요한 메타 데이터만 요청 해야 합니다.
