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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107439"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 및 SQLColAttribute
**SQLDescribeCol** 하 고 **SQLColAttribute** 결과 집합 메타 데이터를 검색 하는 데 사용 됩니다. 이 두 함수 간의 차이점은 **SQLDescribeCol** 같은 다섯 가지 하는 동안 정보 (열 이름, 데이터 형식, 전체 자릿수, 배율 및 null 허용 여부)은 항상 반환 **SQLColAttribute** 단일 응용 프로그램에서 요청 된 정보를 반환 합니다. 그러나 **SQLColAttribute** 보다 다양 한 다양 한 열의 대/소문자 구분을 포함 하 여 메타 데이터를 반환할 수, 크기, 업데이트 가능성 및 검색 가능성을 표시 합니다.  
  
 특히 데이터를 표시 하는 많은 응용 프로그램에서 반환 된 메타 데이터만 필요 **SQLDescribeCol**합니다. 이러한 응용 프로그램에 대 한 것은 더 빠르게 사용할 **SQLDescribeCol** 보다 **SQLColAttribute** 정보를 단일 호출에서 반환 되기 때문입니다. 특히 데이터를 업데이트 하는 다른 응용 프로그램에서 반환 된 추가 메타 데이터를 필요 **SQLColAttribute** 있으므로 두 함수를 사용 합니다. 또한 **SQLColAttribute** 드라이버별 메타 데이터를 지원 하며 자세한 내용은 참조 하십시오 [드라이버별 데이터 형식, 설명자 유형, 정보 유형, 진단 유형 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)합니다.  
  
 응용 프로그램 집합이 닫힐 결과 대해 커서 앞 및 문이 준비 되거나 실행 된 후 언제 든 지 결과 집합 메타 데이터를 검색할 수 있습니다. 매우 적은 응용 프로그램 및 실행 하기 전에 문을 준비 되 면 결과 집합 메타 데이터를 필요 합니다. 가능한 경우 응용 프로그램 메타 데이터를 검색할 때까지 일부 데이터 원본에서 준비 된 문의 메타 데이터를 반환할 수 없습니다. 걸립니다 경우가 드라이버에서이 기능을 에뮬레이션 하기 때문에 문이 실행 된 후 대기 해야 합니다. 드라이버 0 행 결과 대체 하 여 집합을 생성할 수 있습니다 예를 들어,를 **여기서** 절을 **선택** 절을 사용 하 여 문을 **WHERE 1 = 2** 및 실행 합니다 결과 문입니다.  
  
 메타 데이터를 데이터 원본에서 검색 하는 데 비용이 많이 드는 경우가 많습니다. 이 인해 드라이버는 서버에서 검색 하며 유지에 대 한 결과 대해 커서 설정으로 열려 있는 모든 메타 데이터를 캐시 해야 합니다. 또한 응용 프로그램에 반드시 필요한 메타 데이터만 요청 해야 합니다.
