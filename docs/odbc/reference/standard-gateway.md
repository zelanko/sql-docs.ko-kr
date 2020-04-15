---
title: 표준 게이트웨이 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67551845c0dd8c6a28c0c4bc1c50f54ee8232df1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280076"
---
# <a name="standard-gateway"></a>표준 게이트웨이
*게이트웨이는* 한 DBMS를 다른 DBMS처럼 보이게 하는 소프트웨어입니다. 즉, 게이트웨이는 단일 DBMS의 프로그래밍 인터페이스, SQL 문법 및 데이터 스트림 프로토콜을 허용하고 숨겨진 DBMS의 프로그래밍 인터페이스, SQL 문법 및 데이터 스트림 프로토콜로 변환합니다. 예를 들어 Microsoft® SQL Server™를 사용하도록 작성된 응용 프로그램은 마이크로 의사 결정기 DB2 게이트웨이를 통해 DB2 데이터에 액세스할 수도 있습니다. 이 제품으로 인해 DB2가 SQL 서버처럼 보입니다. 게이트웨이를 사용할 때는 각 대상 데이터베이스에 대해 다른 게이트웨이를 작성해야 합니다.  
  
 게이트웨이는 DBMS 간의 아키텍처 차이에 의해 제한되지만 표준화에 적합합니다. 그러나 모든 DBMS가 단일 DBMS의 프로그래밍 인터페이스, SQL 문법 및 데이터 스트림 프로토콜을 표준화하는 경우 DBMS를 표준으로 선택해야 합니까? 물론 어떤 상용 DBMS 공급 업체는 경쟁사의 제품에 표준화에 동의 할 가능성이 없습니다. 또한 표준 프로그래밍 인터페이스, SQL 문법 및 데이터 스트림 프로토콜이 개발되면 게이트웨이가 필요하지 않습니다.
