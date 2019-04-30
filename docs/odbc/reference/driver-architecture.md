---
title: 드라이버 아키텍처 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b593c3bd8619f0fbba47357f312479c2cd14063b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63254235"
---
# <a name="driver-architecture"></a>드라이버 아키텍처
드라이버 아키텍처는 SQL 문 소프트웨어 프로세스에 따라 두 가지 범주로 나누어 집니다.  
  
-   **파일 기반 드라이버** 드라이버 실제 데이터에 직접 액세스 합니다. 이 경우 드라이버는 역할을 드라이버 및 데이터 원본 즉, ODBC 호출 및 SQL 문을 처리합니다. 예를 들어, dBASE 드라이버는 dBASE 드라이버 독립 실행형 데이터베이스 엔진을 사용 하 여 수를 제공 하지 않으므로 파일 기반 드라이버입니다. 파일 기반 드라이버의 개발자가 자신의 데이터베이스 엔진을 작성 해야 하는 것이 반드시 합니다.  
  
-   **DBMS 기반 드라이버** 드라이버 별도 데이터베이스 엔진을 통해 실제 데이터에 액세스 합니다. 드라이버만 ODBC 호출을 처리 하는 경우 전달 SQL 문을 데이터베이스 엔진으로 처리 합니다. 예를 들어, Oracle 드라이버는 Oracle 드라이버를 사용 하 여 독립 실행형 데이터베이스 엔진에 있으므로 DBMS 기반 드라이버입니다. 데이터베이스 엔진 상주 하는 위치는 중요 하지 않습니다. 드라이버와 동일한 컴퓨터 또는 네트워크 상의 다른 컴퓨터에 있을 수 있습니다. 게이트웨이 통해 액세스할 수도 있습니다.  
  
 드라이버 아키텍처는 일반적으로 드라이버 작성자;에 즉, 드라이버 아키텍처 일반적으로 차이가 없습니다 응용 프로그램. 그러나 아키텍처는 응용 프로그램 특정 DBMS SQL을 사용할 수 있는지 여부를 발생할 수 있습니다. 예를 들어, Microsoft Access 독립 실행형 데이터베이스 엔진을 제공합니다. DBMS 기반 Microsoft Access 드라이버는 경우이 엔진-를 통해 데이터 액세스 응용 프로그램을 사용 하 여 Microsoft Access-SQL 문을 처리 엔진에 전달할 수 있습니다.  
  
 그러나 드라이버는 파일 기반-즉, Microsoft® Access.mdb 파일에 직접 액세스 하는 전용 엔진을 포함 하는 경우 Microsoft 액세스 전용 SQL 문을 엔진에 전달 하려고 구문 오류가 발생할 수 있습니다. 이유는 독점 엔진은 ODBC SQL만 구현 하는 일을 할 된다는 것입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [파일 기반 드라이버](../../odbc/reference/file-based-drivers.md)  
  
-   [DBMS 기반 드라이버](../../odbc/reference/dbms-based-drivers.md)  
  
-   [네트워크 예제](../../odbc/reference/network-example.md)  
  
-   [기타 드라이버 아키텍처](../../odbc/reference/other-driver-architectures.md)
