---
title: 드라이버 | 마이크로 소프트 문서
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
ms.openlocfilehash: 7c8b40641be3db34fc6929edecdd5dd923700957
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294186"
---
# <a name="drivers"></a>드라이버
*드라이버는* ODBC API에서 함수를 구현하는 라이브러리입니다. 각각은 특정 DBMS에 만연합니다. 예를 들어 오라클의 드라이버는 Informix DBMS의 데이터에 직접 액세스할 수 없습니다. 드라이버는 기본 DBMS의 기능을 노출합니다. DBMS에서 지원하지 않는 기능을 구현할 필요는 없습니다. 예를 들어 기본 DBMS가 외부 조인을 지원하지 않는 경우 드라이버도 지원하지 않습니다. 유일한 주요 예외는 Xbase와 같은 독립 실행형 데이터베이스 엔진이 없는 DBMS의 드라이버는 최소한 최소한의 SQL을 지원하는 데이터베이스 엔진을 구현해야 한다는 것입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [드라이버 작업](../../odbc/reference/driver-tasks.md)  
  
-   [드라이버 아키텍처](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft 제공 ODBC 드라이버](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
