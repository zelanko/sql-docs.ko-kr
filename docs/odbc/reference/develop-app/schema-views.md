---
title: 스키마 보기 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 782dec08b76a9e5a97719d6af39e2c30c0f92d19
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47797391"
---
# <a name="schema-views"></a>스키마 보기
ODBC 카탈로그 함수를 호출 하 여 또는 INFORMATION_SCHEMA 뷰를 사용 하 여 응용 프로그램 DBMS에서 메타 데이터 정보를 검색할 수 있습니다. 뷰는 ANSI SQL-92 표준에서 정의 됩니다.  
  
 DBMS 및 드라이버에서 지원할 경우, INFORMATION_SCHEMA 뷰 ODBC 카탈로그 함수를 제공 하는 보다 메타 데이터를 검색 하는 강력 하 고 포괄적인 수단을 제공 합니다. 응용 프로그램 자체 사용자 지정을 실행할 수 있습니다 **선택** 이러한 뷰 중 하나에 대해 문을 뷰를 조인할 수 또는 공용 구조체 뷰에 대해 수행할 수 있습니다. 큰 유틸리티 및 광범위 한 메타 데이터를 제공 하는 동안 INFORMATION_SCHEMA 뷰 지원 되지 않습니다 종종 DBMS에 의해. 이 자세한 Dbms 및 드라이버의 규정을 준수 SQL-92에 따라 달라질 수 있습니다.  
  
 뷰 지를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_INFO_SCHEMA_VIEWS 옵션을 사용 합니다. 지원 되는 보기에서 메타 데이터를 검색할 응용 프로그램 실행을 **선택** 필요한 스키마 정보를 지정 하는 문입니다.
