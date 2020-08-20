---
description: 드라이버
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81e8989fc178728e687baa13b37e6055692d9413
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494596"
---
# <a name="drivers"></a>드라이버
*드라이버* 는 ODBC API에서 함수를 구현 하는 라이브러리입니다. 각은 특정 DBMS에만 적용 됩니다. 예를 들어 Oracle 드라이버는 Informix DBMS의 데이터에 직접 액세스할 수 없습니다. 드라이버는 기본 Dbms의 기능을 노출 합니다. DBMS에서 지원 하지 않는 기능을 구현 하는 데 필요 하지 않습니다. 예를 들어 기본 DBMS에서 외부 조인을 지원 하지 않는 경우에는 드라이버를 사용할 수 없습니다. 이에 대 한 유일한 주요 예외는 Xbase와 같이 독립 실행형 데이터베이스 엔진이 없는 Dbms 용 드라이버가 최소한의 SQL을 지 원하는 데이터베이스 엔진을 구현 해야 한다는 것입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [드라이버 작업](../../odbc/reference/driver-tasks.md)  
  
-   [드라이버 아키텍처](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft 제공 ODBC 드라이버](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
