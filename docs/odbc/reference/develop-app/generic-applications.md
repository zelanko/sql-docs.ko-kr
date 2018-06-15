---
title: 일반 응용 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae9643de106e11865505483d84f2253fb9511227
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909528"
---
# <a name="generic-applications"></a>일반 응용 프로그램
일반 응용 프로그램 데이터베이스에서 데이터를 검색 하는 스프레드시트와 같은 하드 코드 된 작업을 수행 하는 경우가 있습니다. 또한 다양 한 사용자가 입력 하 고 SQL 문을 실행할 수 있도록 일반 쿼리 응용 프로그램과 같은 사용자 정의 작업을 수행할 수 있습니다. 어떤 일반 응용 프로그램 서로 공통 되는 이며 다양 한 다른 Dbms와 작동 해야 하는지는 개발자 모르면 미리 이러한 Dbms는 것입니다.  
  
 따라서 일반 응용 프로그램을 높은 상호 운용 가능 해야 합니다. 개발자 기능에 대 한 상호 운용성 이상적일 많은 선택 옵션을 확인 해야 하 고 다양 한 범위의 기능을 지 원하는 드라이버를 기대 되는 코드를 작성 해야 합니다. 인기 있는 Dbms를 작성 하려면 일반 응용 프로그램을 튜닝할 수 수 있습니다 하는 동안 드라이버 관련 또는 DBMS 관련 코드 거의 포함 됩니다.
