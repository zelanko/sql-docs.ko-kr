---
title: 일반 응용 프로그램 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607676d5370f02ee1d39196bff9261bc897521ee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305554"
---
# <a name="generic-applications"></a>일반 애플리케이션
일반 응용 프로그램은 데이터베이스에서 데이터를 검색하는 스프레드시트와 같이 하드 코딩된 작업을 수행하는 경우가 있습니다. 또한 사용자가 SQL 문을 입력하고 실행할 수 있도록 하는 일반 쿼리 응용 프로그램과 같은 다양한 사용자 정의 작업을 수행할 수도 있습니다. 일반적인 응용 프로그램의 공통점은 다양한 DBMS와 함께 작업해야 하며 개발자가 이러한 DBMS가 무엇인지 미리 알지 못한다는 것입니다.  
  
 따라서 일반 응용 프로그램은 상호 운용성이 높아야 합니다. 개발자는 다양한 선택을 해야 하며, 기능에 대한 상호 운용성을 차단해야 하며, 드라이버가 다양한 기능을 지원할 것으로 예상되는 코드를 작성해야 합니다. 일반 응용 프로그램은 인기 있는 DBMS에서 작동하도록 조정될 수 있지만 드라이버별 또는 DBMS 관련 코드를 포함하지 않는 경우는 거의 없습니다.
