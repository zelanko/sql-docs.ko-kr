---
title: SQL 모듈 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30c116878049c4f6a8f36e988731ab641e03c6d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232771"
---
# <a name="sql-modules"></a>SQL 모듈
모듈을 통해 DBMS SQL 문을 보내기 위한 두 번째 방법은 됩니다. 요약 하자면, 모듈 호스트 프로그래밍 언어에서에서 호출 되는 프로시저의 그룹으로 구성 됩니다. 각 프로시저에는 단일 SQL 문을 포함 하 고 데이터에는 프로시저에서 매개 변수를 통해 전달 됩니다.  
  
 모듈을 응용 프로그램 코드에 연결 된 개체 라이브러리로 생각할 수 있습니다. 그러나 구현에 따라 다릅니다는 정확 하 게 하는 방법을 절차 및 응용 프로그램의 나머지 부분 연결 됩니다. 예를 들어 절차 개체 코드를 컴파일 및 응용 프로그램 코드에 직접 연결할 수 없습니다, 컴파일 및 DBMS 및 응용 프로그램 코드에 배치 하는 계획 식별자 액세스에 대 한 호출에 저장할 수 있습니다 또는 런타임에 해석 될 수 있습니다.  
  
 모듈의 주요 이점은 이러한 프로그래밍 언어에서 SQL 문을 완전히 분리 됩니다. 이론적으로 다른 변경 하지 않고 하나를 변경 하 여 단순히 연결을 다시 수 있어야 합니다.
