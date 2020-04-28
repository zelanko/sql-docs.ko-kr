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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cae06efe6dd11e651e8553fa5c1004c2fa145478
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302994"
---
# <a name="ddl-statements"></a>DDL 문
DDL (데이터 정의 언어) 문은 Dbms 간에 크게 다릅니다. ODBC SQL은 테이블, 인덱스 및 뷰를 만들고 삭제 하는 가장 일반적인 데이터 정의 작업에 대 한 문을 정의 합니다. 테이블 변경 및 권한을 부여 하 고 취소 합니다. 다른 모든 DDL 문은 데이터 원본에만 적용 됩니다. 따라서 상호 운용 가능한 응용 프로그램은 일부 데이터 정의 작업을 수행할 수 없습니다. 일반적으로이는 문제가 되지 않습니다. 이러한 작업은 DBMS 마다 고유 하 고 대부분의 Dbms 또는 드라이버와 함께 제공 되는 설치 프로그램과 함께 제공 되는 독점 데이터베이스 관리 소프트웨어에 가장 적합 합니다.  
  
 데이터 정의의 또 다른 문제는 데이터 형식 이름이 Dbms 마다 다른 크게는 것입니다. **SQLGetTypeInfo** 는 표준 데이터 형식 이름을 정의 하 고 드라이버를 실행 하 여 dbms 관련 이름으로 변환 하는 대신 응용 프로그램에서 dbms 관련 데이터 형식 이름을 검색할 수 있는 방법을 제공 합니다. 상호 운용 가능한 응용 프로그램은 SQL 문에 이러한 이름을 사용 하 여 테이블을 만들고 변경 해야 합니다. [부록 C: SQL 문법](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)및 [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)에 나열 된 이름은 예일 뿐입니다.
