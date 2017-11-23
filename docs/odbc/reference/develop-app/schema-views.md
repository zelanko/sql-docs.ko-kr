---
title: "스키마 뷰 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d85a59f54fab5508c5781bfb29a1243c12b44e6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="schema-views"></a>스키마 뷰
ODBC 카탈로그 함수를 호출 하 여 또는 INFORMATION_SCHEMA 뷰를 사용 하 여 응용 프로그램 DBMS에서 메타 데이터 정보를 검색할 수 있습니다. 뷰는 ANSI sql-92 표준에서 정의 됩니다.  
  
 DBMS와 드라이버에서 지원할 경우, INFORMATION_SCHEMA 뷰 메타 데이터를 제공 하는 ODBC 카탈로그 함수 보다 검색 하는 강력 하 고 포괄적인 수단을 제공 합니다. 응용 프로그램 자체의 사용자 지정을 실행할 수 있습니다 **선택** 이러한 뷰 중 하나에 대해 문의 뷰를 조인할 수 또는 공용 구조체 뷰에 대해 수행할 수 있습니다. 큰 유틸리티 및 광범위 한 메타 데이터를 제공 하는 동안 INFORMATION_SCHEMA 뷰 지원 되지 않습니다 종종는 DBMS에 의해. 이 더 많은 Dbms 및 드라이버 SQL 92에 맞게 준수를 실현 하는 대로 변경 될 수 있습니다.  
  
 사용할 수 있는 보기를 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_INFO_SCHEMA_VIEWS 옵션을 사용 합니다. 메타 데이터에서 지원 되는 뷰를 검색 하려면 응용 프로그램을 실행 한 **선택** 필요한 스키마 정보를 지정 하는 문입니다.
