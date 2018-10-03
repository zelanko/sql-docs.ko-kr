---
title: 표준 게이트웨이 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c70a558b065765dd9f8c0895345959e8aa22ebfe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854028"
---
# <a name="standard-gateway"></a>표준 게이트웨이
A *게이트웨이* 는 다른 모양 하나 DBMS는 소프트웨어입니다. 즉, 게이트웨이 프로그래밍 인터페이스, SQL 문법, 및 데이터 스트림 하는 단일 dbms 프로토콜 및 프로그래밍 인터페이스에 SQL 문법, 변환 받아들이고 데이터 스트림 프로토콜 숨겨진된 DBMS의 합니다. 예를 들어, Microsoft® SQL Server™를 사용 하도록 작성 된 응용 프로그램 데이터에 액세스할 수도 DB2 마이크로 Decisionware DB2 게이트웨이; 이 제품에는 SQL Server 같은 DB2 발생 합니다. 게이트웨이 사용 하는 경우 각 대상 데이터베이스에 대 한 다른 게이트웨이 작성 합니다.  
  
 게이트웨이 Dbms 간의 아키텍처 차이 의해 제한 됩니다, 하더라도 좋은 후보인 표준화 됩니다. 그러나 모든 Dbms 프로그래밍 인터페이스를 표준화할 수 인 경우 SQL 문법 및 데이터 스트림 프로토콜 해당 DBMS는 표준으로 선택 하는 단일 dbms? 확실히 없는 상업용 DBMS 공급 업체는 경쟁 업체의 제품에서 표준화에 동의 하 가능성이 높습니다. 및 표준 프로그래밍 인터페이스, SQL 문법 및 데이터 스트림 프로토콜 개발 하는 경우 게이트웨이가 필요 합니다.
