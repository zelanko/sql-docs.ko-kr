---
title: "제품 주기의 길이 | Microsoft Docs"
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
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c363ecd47545868e2d40afabdce9bbef6f78031
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="length-of-the-product-cycle"></a>제품 주기의 길이
상호 운용성에 대 한 마지막 문의 시간입니다. 일반적으로 상호 운용 가능한 응용 프로그램을 개발 noninteroperable 하나 개발 보다 오래 걸립니다. 이유는 응용 프로그램 해야 DBMS 기능을 확인, 다른 Dbms에 대 한 동일한 작업을 다르게 수행, 다른 하지만 일부 Dbms에서 지 원하는 기능을 해결 등입니다.  
  
 개발 시간 외에도 제품 수명 고려 되어야 합니다. 응용 프로그램 간에 하나 DBMS에서 마이그레이션할 경우 데이터를 전송 하는 응용 프로그램과 같이 한 번 사용 하도록 디자인 된 경우 상호 운용할 수 있도록 위치가 있는데 합니다. 응용 프로그램이 한 번 사용 하 고 삭제 됩니다.  
  
 응용 프로그램 시간이 오래 존재 하며, 상호 운용 가능한 응용 프로그램으로 관리가 수도 있습니다. 대상으로 단일 DBMS에 있는 사용자 지정 응용 프로그램에도 마찬가지입니다. 이유 코드 상호 운용 가능한 데이터베이스 기능 제한 된 하위 집합을 사용 한다는 것을입니다. 원본 DBMS에 대 한 변경 하는 경우에 사용할 수 있는 이러한 기능을 유지 하려면 드라이버가 필요 합니다. 따라서 상호 운용할 수 있는 코드에서 드라이버 개발자에 게 응용 프로그램 개발자는 DBMS에 대처 변경 하는 것의 부담을 바꿀 수 있습니다.

