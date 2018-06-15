---
title: SQLDescribeCol 및 SQLColAttribute | Microsoft Docs
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
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a99551fd76b68af9d48b5d97f8ef696259c8661e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914018"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 및 SQLColAttribute
**SQLDescribeCol** 및 **SQLColAttribute** 결과 집합 메타 데이터를 검색 하는 데 사용 됩니다. 이 두 기능 간의 차이점은 **SQLDescribeCol** 정보 (열 이름, 데이터 형식, 정밀도, 배율 및 null 허용 여부)을 하는 동안 동일한 5 가지 구성 요소는 항상 반환 **SQLColAttribute** 는 단일 응용 프로그램에서 요청 된 정보를 반환 합니다. 그러나 **SQLColAttribute** 반환할 메타 데이터를 열의 대/소문자 구분을 포함 하 여 보다 다양 한 선택, 크기, 업데이트 가능성 및 검색 기능은 표시 수 있습니다.  
  
 데이터를 표시 하기만 하는 특히 된 많은 응용 프로그램에서 반환 된 메타 데이터에만 필요 **SQLDescribeCol**합니다. 이러한 응용 프로그램에 대 한 것은 더 빠르게 사용할 **SQLDescribeCol** 보다 **SQLColAttribute** 정보 단일 호출에서 반환 되기 때문입니다. 데이터를 업데이트 하는 특히 된 다른 응용 프로그램에서 반환 된 추가 메타 데이터를 필요한 **SQLColAttribute** 이므로 두 함수를 사용 하 여 합니다. 또한 **SQLColAttribute** 드라이버 관련 메타 데이터를 지원 하며 자세한 내용은 참조 [드라이버 관련 데이터 형식, 형식 설명자, 정보 유형, 진단 형식 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)합니다.  
  
 응용 프로그램 및 결과 위에 커서 앞 집합이 닫힐 문이 준비 되거나 실행 된 후 언제 든 지 결과 집합 메타 데이터를 검색할 수 있습니다. 매우 적은 응용 프로그램 및 실행 하기 전에 문을 준비 된 후 결과 집합 메타 데이터에 필요 합니다. 가능 하면 응용 프로그램 메타 데이터를 검색할 때까지 일부 데이터 원본에서 준비 된 문의 메타 데이터를 반환할 수 없습니다 느리게 처리 방식은 드라이버에서이 기능을 에뮬레이션 하기 때문에 문이 실행 된 후 대기 해야 합니다. 예를 들어 드라이버 대체 하 여 설정 된 0 행 결과 생성할 수 있습니다는 **여기서** 절은 **선택** 문 절과 함께 **WHERE 1 = 2** 실행 하는 결과 문입니다.  
  
 메타 데이터는 데이터 원본에서 검색 하는 데 비용이 경우가 많습니다. 이 인해 드라이버는 모든 메타 데이터에 대 한 커서가 결과 집합으로 열려 있기 보유 고 서버에서 검색을 캐시 해야 합니다. 또한 응용 프로그램에 반드시 필요한 메타 데이터에만 요청 해야 합니다.
