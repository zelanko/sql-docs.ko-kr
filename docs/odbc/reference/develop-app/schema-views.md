---
title: 스키마 뷰 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1a9e421c4835d35e3c4f3c644e69b8c7601e8e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304254"
---
# <a name="schema-views"></a>스키마 보기
응용 프로그램은 ODBC 카탈로그 함수를 호출하거나 INFORMATION_SCHEMA 뷰를 사용하여 DBMS에서 메타데이터 정보를 검색할 수 있습니다. 뷰는 ANSI SQL-92 표준에 의해 정의됩니다.  
  
 DBMS 및 드라이버에서 지원하는 경우 INFORMATION_SCHEMA 보기는 ODBC 카탈로그 함수가 제공하는 것보다 더 강력하고 포괄적인 메타데이터 검색 수단을 제공합니다. 응용 프로그램은 이러한 보기 중 하나에 대해 자체 사용자 지정 **SELECT** 문을 실행하거나, 뷰를 조인하거나, 뷰에서 공용 구조조정을 수행할 수 있습니다. 더 큰 유용성과 광범위한 메타데이터를 제공하면서 INFORMATION_SCHEMA 보기는 종종 DBMS에서 지원되지 않습니다. 더 많은 DBMS와 드라이버가 SQL-92를 준수함에 따라 이러한 변경이 발생할 수 있습니다.  
  
 지원되는 뷰를 결정하기 위해 응용 프로그램은 SQL_INFO_SCHEMA_VIEWS 옵션을 사용하여 **SQLGetInfo를** 호출합니다. 지원되는 보기에서 메타데이터를 검색하기 위해 응용 프로그램은 필요한 스키마 정보를 지정하는 **SELECT** 문을 실행합니다.
