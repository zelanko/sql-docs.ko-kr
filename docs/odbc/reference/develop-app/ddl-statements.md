---
title: DDL 문 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9100405c91387faa66b714a94b8259167ae31899
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542678"
---
# <a name="ddl-statements"></a>DDL 문
DDL (데이터 정의 언어) 문이 Dbms 간에 크게 다릅니다. ODBC SQL 문을 가장 일반적인 데이터 정의 작업에 대 한 정의: 만들기 및 테이블, 인덱스 및; 뷰를 삭제 합니다. 테이블 변경 부여 및 권한을 취소 합니다. 모든 다른 DDL 문과 데이터 소스 관련 됩니다. 따라서 상호 운용 가능한 응용 프로그램 일부 데이터 정의 작업을 수행할 수 없습니다. 일반적으로 문제가 되지 않습니다, 그리고 이러한 작업 항상 DBMS 관련 경향이 최상의 이기 때문에 대부분의 Dbms와 함께 제공 되는 전용 데이터베이스 관리 소프트웨어에는 왼쪽 또는 드라이버를 사용 하 여 설치 프로그램을 제공 합니다.  
  
 데이터 정의 있는 또 다른 문제 이름을 다릅니다 단시간 Dbms 간에 데이터 형식이 해당 합니다. 대신 표준 데이터 형식 이름을 정의 하 고 DBMS 특정 이름으로 변환 하기 위해 드라이버를 강제로 **SQLGetTypeInfo** DBMS 특정 데이터 형식 이름을 검색 하려면 응용 프로그램에 대 한 방법을 제공 합니다. 상호 운용 가능한 응용 프로그램 만들고 테이블을 변경 하려면 SQL 문에서 이러한 이름에 사용 해야 에 나열 된 이름을 [부록 c: SQL 문법을](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), 및 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)은 예일 뿐입니다.
