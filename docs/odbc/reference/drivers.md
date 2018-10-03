---
title: 드라이버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e3996aafa0e4f5b389e4f46d5df3b22632daad9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710041"
---
# <a name="drivers"></a>드라이버
*드라이버* ODBC api에서 함수를 구현 하는 라이브러리입니다. 각각은 특정 DBMS;에 특정 예를 들어, Oracle 드라이버는 Informix DBMS의 데이터에 직접 액세스할 수 없습니다. 기본 Dbms;의 기능을 노출 하는 드라이버 DBMS에 의해 지원 하지 않는 기능이 구현 않아도 함께 제공 됩니다. 예를 들어, 외부 조인, 다음 모두 기본 DBMS를 지원 하지 않는 경우 드라이버를 해야 합니다. 유일한 주요 예외는 Xbase와 같은 독립 실행형 데이터베이스 엔진에 없는 Dbms 용 드라이버 최소한 SQL 최소 크기를 지 원하는 데이터베이스 엔진을 구현 해야 하는 경우  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [드라이버 작업](../../odbc/reference/driver-tasks.md)  
  
-   [드라이버 아키텍처](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 제공 ODBC 드라이버](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
