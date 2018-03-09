---
title: "SQL 모듈 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aac70e91e91277f7778fed439f68e5620f116d41
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sql-modules"></a>SQL 모듈
DBMS SQL 문을 보내기 위한 두 번째 방법은 모듈을 통해 것입니다. 짧게 모듈은 호스트 프로그래밍 언어에서에서 호출 된 프로시저의 그룹으로 구성 됩니다. 각 프로시저는 단일 SQL 문 있어서 데이터가 하 고 프로시저에서 매개 변수를 통해 전달 됩니다.  
  
 모듈을 응용 프로그램 코드에 연결 된 개체 라이브러리로 생각할 수 있습니다. 그러나 정확 하 게 프로시저와 응용 프로그램의 나머지과 연결 된 방법을 구현에 따라 다릅니다. 예를 들어 프로시저를 개체 코드로 컴파일될와 응용 프로그램 코드에 직접 연결할 수 없습니다, 컴파일 및 DBMS 및 응용 프로그램 코드에 배치 하는 계획 식별자 액세스에 대 한 호출에 저장 된 수 또는 런타임 시 해석 될 수 있습니다.  
  
 모듈의 주요 장점은 프로그래밍 언어에서 SQL 문의 명확 하 게 구분 하는 것입니다. 이론적으로, 다른 변경 하지 않고 하나를 변경 하 여 단순히 다시 연결 수 있어야 합니다.
