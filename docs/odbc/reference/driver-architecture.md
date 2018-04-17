---
title: 드라이버 아키텍처 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa23b4a900e0415268746b84b94d68ea8492bbca
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="driver-architecture"></a>드라이버 아키텍처
드라이버 아키텍처는 SQL 문에 있는 소프트웨어 프로세스에 따라 두 가지 범주에 해당 됩니다.  
  
-   **파일 기반 드라이버** 드라이버는 물리적 데이터를 직접 액세스 합니다. 이 경우 드라이버와 역할을 모두 드라이버 데이터 소스 즉, ODBC 호출 및 SQL 문을 처리합니다. 예를 들어 dBASE 드라이버는 독립 실행형 데이터베이스 엔진 드라이버 צ ְ ײ dBASE 제공 하지 않기 때문에 파일 기반 드라이버. 파일 기반 드라이버의 개발자가 자신의 데이터베이스 엔진을 작성 해야 하는 것이 유용 합니다.  
  
-   **DBMS 기반 드라이버** 드라이버 별도 데이터베이스 엔진을 통해 실제 데이터에 액세스 합니다. 이 경우에 드라이버가 처리만 ODBC 호출; SQL 문을에 전달 하도록 데이터베이스 엔진을 처리 합니다. 예를 들어 Oracle 드라이버를 사용 하 여 독립 실행형 데이터베이스 엔진에 있기 때문에 Oracle 드라이버는 DBMS 기반 드라이버. 데이터베이스 엔진이 있는 위치는 중요 하지 않습니다. 드라이버와 동일한 컴퓨터 또는 네트워크에서 다른 컴퓨터에 있을 수합니다 있습니다. 게이트웨이 통해 액세스할 수도 있습니다.  
  
 드라이버 작성자; 에게만 드라이버 아키텍처 일반적으로 흥미롭습니다. 즉, 드라이버 아키텍처에는 일반적으로 응용 프로그램에 중요를 하지 않습니다. 그러나 아키텍처는 응용 프로그램이 특정 DBMS SQL을 사용할 수 있는지 여부를 발생할 수 있습니다. 예를 들어 Microsoft Access 데이터베이스는 독립 실행형 데이터베이스 엔진을 제공합니다. Microsoft Access 드라이버는 DBMS 기반 하는 경우-이 엔진을 통해 데이터 액세스-응용 프로그램 처리를 위해 엔진에 Microsoft Access-SQL 문을 전달할 수 있습니다.  
  
 그러나 파일 기반 드라이버가 경우-즉, Microsoft® Access.mdb 파일을 직접 액세스 하는 전용 엔진을 포함-Microsoft Access-전용 SQL 문을 엔진에 전달 하려고 구문 오류가 발생할 가능성이 높습니다. 이유 전용 엔진만 ODBC SQL을 구현할 가능성이 된다는 점입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [파일 기반 드라이버](../../odbc/reference/file-based-drivers.md)  
  
-   [DBMS 기반 드라이버](../../odbc/reference/dbms-based-drivers.md)  
  
-   [네트워크 예제](../../odbc/reference/network-example.md)  
  
-   [기타 드라이버 아키텍처](../../odbc/reference/other-driver-architectures.md)
