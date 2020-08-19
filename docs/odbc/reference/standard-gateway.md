---
description: 표준 게이트웨이
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 687097813d01b27ac49e657f11a2b763e2ca1214
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448903"
---
# <a name="standard-gateway"></a>표준 게이트웨이
*게이트웨이* 는 하나의 DBMS가 다른 DBMS와 같이 보이도록 하는 소프트웨어의 일부입니다. 즉, 게이트웨이는 단일 DBMS의 프로그래밍 인터페이스, SQL 문법 및 데이터 스트림 프로토콜을 수락 하 고이를 숨겨진 DBMS의 프로그래밍 인터페이스, SQL 문법 및 데이터 스트림 프로토콜로 변환 합니다. 예를 들어 Microsoft® SQL Server™ 사용 하도록 작성 된 응용 프로그램은 마이크로 Decisionware DB2 게이트웨이를 통해 DB2 데이터에 액세스할 수도 있습니다. 이 제품을 통해 DB2는 SQL Server 같이 표시 됩니다. 게이트웨이를 사용 하는 경우 각 대상 데이터베이스에 대해 다른 게이트웨이를 작성 해야 합니다.  
  
 게이트웨이는 Dbms 간의 아키텍처 차이로 제한 되지만 표준화에 적합 합니다. 그러나 모든 dbms를 표준으로 선택 해야 하는 단일 DBMS의 프로그래밍 인터페이스, SQL 문법 및 데이터 스트림 프로토콜에서 표준화 하려면 어떻게 해야 하나요? 물론 상업적 DBMS 공급 업체는 경쟁 업체의 제품을 표준화 하는 데 동의할 수 있습니다. 표준 프로그래밍 인터페이스, SQL 문법 및 데이터 스트림 프로토콜이 개발 되는 경우에는 게이트웨이가 필요 하지 않습니다.
