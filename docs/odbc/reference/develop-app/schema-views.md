---
title: 스키마 뷰 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e2dd512ab529f1fb5d216f4a2e459cd601d40e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67943752"
---
# <a name="schema-views"></a>스키마 보기
응용 프로그램은 ODBC 카탈로그 함수를 호출 하거나 INFORMATION_SCHEMA 뷰를 사용 하 여 DBMS에서 메타 데이터 정보를 검색할 수 있습니다. 뷰는 ANSI SQL-92 표준에 의해 정의 됩니다.  
  
 DBMS 및 드라이버에서 지 원하는 경우 INFORMATION_SCHEMA 뷰는 ODBC 카탈로그 함수에서 제공 하는 것 보다 더 강력 하 고 포괄적인 메타 데이터 검색 방법을 제공 합니다. 응용 프로그램은 이러한 뷰 중 하나에 대해 고유한 사용자 지정 **select** 문을 실행 하거나, 뷰를 조인 하거나, 뷰에서 union을 수행할 수 있습니다. 더 큰 유틸리티와 광범위 한 메타 데이터를 제공 하는 동안 INFORMATION_SCHEMA 보기는 DBMS에서 지원 되지 않는 경우가 많습니다. 이는 더 많은 Dbms 및 드라이버가 SQL-92를 준수 하기 때문에 변경 될 수 있습니다.  
  
 지원 되는 뷰를 확인 하기 위해 응용 프로그램은 SQL_INFO_SCHEMA_VIEWS 옵션으로 **SQLGetInfo** 를 호출 합니다. 지원 되는 뷰에서 메타 데이터를 검색 하기 위해 응용 프로그램은 필요한 스키마 정보를 지정 하는 **select** 문을 실행 합니다.
