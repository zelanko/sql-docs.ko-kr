---
title: DDL 선언문 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302994"
---
# <a name="ddl-statements"></a>DDL 문
데이터 정의 언어(DDL) 문은 DBMS에 따라 크게 다릅니다. ODBC SQL은 테이블, 인덱스 및 뷰 를 만들고 삭제하는 가장 일반적인 데이터 정의 작업에 대한 문을 정의합니다. 테이블 변경; 권한을 부여하고 취소할 수 있습니다. 다른 모든 DDL 문은 데이터 원본에 따라 다릅니다. 따라서 상호 운용 가능한 응용 프로그램은 일부 데이터 정의 작업을 수행할 수 없습니다. 일반적으로 이러한 작업은 DBMS에 따라 매우 높은 경향이 있으며 대부분의 DBMS 또는 드라이버와 함께 제공되는 설치 프로그램과 함께 제공되는 독점 데이터베이스 관리 소프트웨어에 가장 적합하기 때문에 문제가 되지 않습니다.  
  
 데이터 정의의 또 다른 문제는 데이터 형식 이름이 DBMS마다 엄청나게 다양하다는 것입니다. **SQLGetTypeInfo는** 표준 데이터 형식 이름을 정의하고 드라이버가 DBMS 별 이름으로 변환하도록 하는 대신 응용 프로그램에서 DBMS 별 데이터 형식 이름을 검색하는 방법을 제공합니다. 상호 운용 가능한 응용 프로그램은 SQL 문에서 이러한 이름을 사용하여 테이블을 만들고 변경해야 합니다. [부록 C: SQL 문법](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)및 [부록 D: 데이터 형식에](../../../odbc/reference/appendixes/appendix-d-data-types.md)나열된 이름은 예제일 뿐입니다.
