---
title: "DDL 문 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4ebd19e39919265d2161927056bb9a4ebb9d55c2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="ddl-statements"></a>DDL 문
데이터 정의 언어 (DDL) 문을 Dbms 매우 다양합니다. ODBC SQL 문을 가장 일반적인 데이터 정의 작업에 대 한 정의: 만들고 테이블, 인덱스, 및; 뷰를 삭제 합니다. 테이블 변경 부여 및 권한을 취소 합니다. 다른 모든 DDL 문은 데이터 원본에 따른 특정입니다. 따라서 상호 운용 가능한 응용 프로그램 일부 데이터 정의 작업을 수행할 수 없습니다. 일반적으로 이것은 문제, 이러한 작업 높은 DBMS 관련 경향이 하며 가장 독점 데이터베이스 관리 소프트웨어에는 왼쪽 대부분 Dbms와 함께 제공 되 또는 드라이버와 함께 제공 되는 설치 프로그램입니다.  
  
 데이터 정의 있는 또 다른 문제는 이름에 따라 다를 매우 Dbms 해당 데이터 형식. 표준 데이터 형식 이름을 정의 하 고 특정 DBMS 이름으로 변환 하기 위해 드라이버를 강제 적용 하지 않고 **SQLGetTypeInfo** DBMS 특정 데이터 형식 이름을 검색 하려면 응용 프로그램에 대 한 방법을 제공 합니다. 상호 운용 가능한 응용 프로그램을 만들고 테이블; 변경 SQL 문에서 이러한 이름에 사용 해야 에 나열 된 이름을 [부록 c: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), 및 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md), 예일 뿐입니다.

