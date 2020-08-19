---
description: SQL(구조적 쿼리 언어)(Structured Query Language)
title: 구조적 쿼리 언어 (SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c68f14bd3e1ae5df29f52332d29393bf15c3b665
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428975"
---
# <a name="structured-query-language-sql"></a>SQL(구조적 쿼리 언어)(Structured Query Language)
일반적인 DBMS를 사용 하면 사용자가 구성 된 효율적인 방식으로 데이터를 저장, 액세스 및 수정할 수 있습니다. 원래 Dbms의 사용자는 프로그래머 였습니다. COBOL과 같은 프로그래밍 언어로 프로그램을 작성 하는 데 필요한 저장 된 데이터에 액세스 합니다. 이러한 프로그램은 종종 사용자에 게 친숙 한 사용자에 게 친숙 한 인터페이스를 제공 하기 위해 작성 되었지만, 데이터 자체에 대 한 액세스는 전문 프로그래머의 서비스에 필요 합니다. 데이터에 대 한 액세스는 실용적이 지 않습니다.  
  
 사용자는 이러한 상황에 전적으로 만족 하지 않았습니다. 데이터에 액세스할 수 있는 동안에는 DBMS 프로그래머가 특수 소프트웨어를 작성 하는 것을 설득 해야 하는 경우가 많습니다. 예를 들어 판매 부서에서 각 영업 사원의 이전 달에 총 판매량을 확인 하 고이 정보를 주문 하 여 회사의 각 판매 직원의 서비스 수를 확인 하려는 경우, 정확 하 게 이러한 방식으로 해당 정보에 액세스할 수 있도록 이미 있었던 프로그램이 있거나, 부서에서 이러한 프로그램을 작성 하도록 프로그래머에 게 요청 해야 합니다. 대부분의 경우이는 가치가 있는 것 보다 더 많은 작업을 수행 하 고, 일회성 또는 임시 조회에 대해 항상 비용이 많이 드는 솔루션 이었습니다. 더 많은 사용자가 쉽게 액세스할 수 있으므로이 문제는 더 크고 더 커졌습니다.  
  
 사용자가 원하는 방식으로 데이터에 액세스할 수 있도록 하 여 요청을 표현할 수 있는 언어를 제공 합니다. 데이터베이스에 대 한 단일 요청은 쿼리로 정의 됩니다. 이러한 언어를 쿼리 언어 라고 합니다. 이러한 목적을 위해 많은 쿼리 언어를 개발 했지만, 이러한 언어 중 하나는 1970 년대 IBM에서 가장 인기 있는 구조적 쿼리 언어입니다. 이는 머리글자어, SQL에서 더 일반적으로 알려져 있으며 "ell" 및 "sequel"로 모두 발음 됩니다. SQL은 1986의 ANSI 표준 이며 1987의 ISO 표준입니다. 오늘날 매우 많은 데이터베이스 관리 시스템에서 사용 됩니다.  
  
 SQL은 사용자의 임시 요구를 해결 했지만 컴퓨터 프로그램의 데이터 액세스가 필요한 것은 아닙니다. 실제로 대부분의 데이터베이스 액세스는 정기적으로 예약 된 보고서와 통계 분석, 주문 항목에 사용 되는 것과 같은 데이터 입력 프로그램, 계정을 조정 하 고 작업 순서를 생성 하는 데 사용 되는 프로그램 등의 데이터 조작 프로그램에서 프로그래밍 방식으로 실행 되 고 있습니다.  
  
 이러한 프로그램은 다음 세 가지 방법 중 하나를 사용 하 여 SQL도 사용 합니다.  
  
-   SQL 문이 C 또는 COBOL과 같은 호스트 언어에 포함 된 **포함 된 sql**입니다.  
  
-   Sql **모듈**-DBMS에서 컴파일되고 호스트 언어에서 호출 되는 sql 문입니다.  
  
-   **호출 수준 인터페이스**또는 CLI-SQL 문을 dbms에 전달 하 고 dbms에서 결과를 검색 하기 위해 호출 하는 함수로 구성 됩니다.  
  
> [!NOTE]  
>  응용 프로그램 프로그래밍 인터페이스 (API) 대신 용어 호출 수준 인터페이스를 사용 하 여 동일한 작업을 수행 하는 것이 과거입니다. 데이터베이스 세계에서 API는 SQL 자체를 설명 하는 데 사용 됩니다. SQL은 DBMS에 대 한 API입니다.  
  
 이러한 선택 항목 중에서 가장 일반적으로 사용 되는 대부분의 Dbms는 독점적인 CLIs를 지원 하지만 가장 일반적으로 사용 됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQL 문 처리](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [Embedded SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 모듈](../../odbc/reference/sql-modules.md)  
  
-   [호출 수준 인터페이스](../../odbc/reference/call-level-interfaces.md)
