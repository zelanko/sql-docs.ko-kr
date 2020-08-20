---
description: 메타데이터는 어떻게 사용되나요?
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca61677b0001ba4c39f81f80f6e3cbce26f27910
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476635"
---
# <a name="how-is-metadata-used"></a>메타데이터는 어떻게 사용되나요?
애플리케이션에서는 대부분의 결과 집합 작업에 대해 메타데이터를 요구합니다. 예를 들어 애플리케이션에서는 열의 데이터 형식을 사용하여 해당 열에 바인딩할 변수의 종류를 확인하고 문자 열의 바이트 길이를 사용 하 여 해당 열의 데이터를 표시 하는 데 필요한 공간의 크기를 결정 합니다. 애플리케이션에서 열의 메타데이터를 확인하는 방법은 애플리케이션 종류에 따라 다릅니다.  
  
 수직 응용 프로그램은 미리 정의 된 테이블로 작업 하 고 해당 테이블에 대해 미리 정의 된 작업을 수행 합니다. 이러한 응용 프로그램에 대 한 결과 집합 메타 데이터는 응용 프로그램을 작성 하기 전에 정의 되 고 응용 프로그램 개발자가 제어 하기 때문에 응용 프로그램에 하드 코딩 될 수 있습니다. 예를 들어 주문 ID 열이 데이터 원본에 4바이트 정수로 정의된 경우 애플리케이션에서는 항상 해당 열에 4바이트 정수를 바인딩할 수 있습니다. 메타데이터가 애플리케이션에 하드 코딩되면 애플리케이션에서 사용하는 테이블의 변경은 일반적으로 애플리케이션 코드의 변경을 암시합니다. 이러한 변경 내용은 응용 프로그램의 새 릴리스의 일부로 일반적으로 적용 되기 때문에 문제가 거의 발생 하지 않습니다.  
  
 수직 응용 프로그램 처럼 사용자 지정 응용 프로그램은 일반적으로 미리 정의 된 테이블에서 작업 하 고 해당 테이블에서 미리 정의 된 작업을 수행 합니다 예를 들어 응용 프로그램을 작성 하 여 세 가지 데이터 원본 간에 데이터를 전송할 수 있습니다. 일반적으로 응용 프로그램을 작성할 때 전송 될 데이터를 알 수 있습니다. 따라서 사용자 지정 응용 프로그램은 하드 코드 된 메타 데이터를 포함 하는 경향이 있습니다.  
  
 일반적으로 임시 쿼리를 지 원하는 제네릭 응용 프로그램은 자신이 만드는 결과 집합의 메타 데이터를 거의 알지 못합니다. 따라서 다음 섹션인 [SQLDescribeCol 및 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)에 설명 된 **Sqlnumresultcols**, **SQLDescribeCol**및 **sqlcolattribute**함수를 사용 하 여 런타임에 메타 데이터를 검색 해야 합니다.  
  
 형식에 관계 없이 모든 응용 프로그램은 카탈로그 함수에서 반환 하는 결과 집합에 대 한 메타 데이터를 하드 코딩할 수 있습니다. 이러한 결과 집합은이 설명서의 참조 섹션에서 정의 됩니다.
