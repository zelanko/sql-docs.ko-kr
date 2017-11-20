---
title: "표준 게이트웨이 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9375bc6bf5054bdfeddd4fc5e53a1494d74eb88b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="standard-gateway"></a>표준 게이트웨이
A *게이트웨이* 다른 모양 하나의 DBMS 시키는 소프트웨어의 일부분이 됩니다. 즉, 게이트웨이 프로그래밍 인터페이스, SQL 문법 및 데이터 스트림 단일 DBMS의 프로토콜 및 프로그래밍 인터페이스 SQL 문법 변환 받아들이고 데이터 스트림 숨겨진된 DBMS의 프로토콜 합니다. 예를 들어 Microsoft® SQL Server™를 사용 하도록 작성 된 응용 프로그램 데이터에 액세스할 수도 DB2 마이크로 Decisionware DB2 게이트웨이; 이 제품에는 d b 2를 SQL Server 같이 하면 됩니다. 게이트웨이 사용 하는 경우 다른 게이트웨이 각 대상 데이터베이스에 대해 작성 되어야 합니다.  
  
 게이트웨이 Dbms 간의 구조적 차이로 제한, 않더라도 표준화 하는 것이 좋습니다. 그러나 모든 Dbms 프로그래밍 인터페이스를 표준화할 수 인 SQL 문법 및 데이터 스트림 프로토콜을 표준으로 선택 하려면 해당 DBMS는 단일 DBMS의? 확실히 없는 상용 DBMS 공급 업체는 경쟁 업체의 제품에서 표준화 하기로 수 있습니다. 한 표준 프로그래밍 인터페이스, SQL 문법 및 데이터 스트림 프로토콜은 개발 하는 경우 게이트웨이가 필요 합니다.

