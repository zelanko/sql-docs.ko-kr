---
title: 드라이버 아키텍처 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ffe2023f028357468700b9bd995d22129ba06817
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294223"
---
# <a name="driver-architecture"></a>드라이버 아키텍처
드라이버 아키텍처는 SQL 문을 처리하는 소프트웨어에 따라 두 가지 범주로 나뉩니다.  
  
-   **파일 기반 드라이버** 드라이버는 물리적 데이터에 직접 액세스합니다. 이 경우 드라이버는 드라이버와 데이터 원본 모두역할을 합니다. 즉, ODBC 호출 및 SQL 문을 처리합니다. 예를 들어 dBASE 드라이버는 dBASE가 드라이버가 사용할 수 있는 독립 실행형 데이터베이스 엔진을 제공하지 않기 때문에 파일 기반 드라이버입니다. 파일 기반 드라이버 개발자는 자체 데이터베이스 엔진을 작성해야 합니다.  
  
-   **DBMS 기반 드라이버** 드라이버는 별도의 데이터베이스 엔진을 통해 물리적 데이터에 액세스합니다. 이 경우 드라이버는 ODBC 호출만 처리합니다. 처리를 위해 데이터베이스 엔진에 SQL 문을 전달합니다. 예를 들어 오라클 드라이버는 드라이버가 사용하는 독립 실행형 데이터베이스 엔진을 가지고 있기 때문에 DBMS 기반 드라이버입니다. 데이터베이스 엔진이 있는 곳은 중요하지 않습니다. 드라이버 또는 네트워크의 다른 컴퓨터와 동일한 컴퓨터에 상주할 수 있습니다. 게이트웨이를 통해 액세스할 수도 있습니다.  
  
 드라이버 아키텍처는 일반적으로 드라이버 작성자만 흥미롭습니다. 즉, 드라이버 아키텍처는 일반적으로 응용 프로그램에 아무런 차이가 없습니다. 그러나 아키텍처는 응용 프로그램이 DBMS 관련 SQL을 사용할 수 있는지 여부에 영향을 줄 수 있습니다. 예를 들어 Microsoft Access는 독립 실행형 데이터베이스 엔진을 제공합니다. Microsoft Access 드라이버가 DBMS 기반인 경우 이 엔진을 통해 데이터에 액세스하는 경우 응용 프로그램은 처리를 위해 Microsoft Access-SQL 문을 엔진에 전달할 수 있습니다.  
  
 그러나 드라이버가 파일 기반인 경우, 즉 Microsoft® Access .mdb 파일에 직접 액세스하는 독점 엔진이 포함되어 있는 경우 Microsoft Access 관련 SQL 문을 엔진에 전달하려는 시도는 구문 오류가 발생할 수 있습니다. 그 이유는 독점 엔진이 ODBC SQL만 구현할 가능성이 있기 때문입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [파일 기반 드라이버](../../odbc/reference/file-based-drivers.md)  
  
-   [DBMS 기반 드라이버](../../odbc/reference/dbms-based-drivers.md)  
  
-   [네트워크 예제](../../odbc/reference/network-example.md)  
  
-   [기타 드라이버 아키텍처](../../odbc/reference/other-driver-architectures.md)
