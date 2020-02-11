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
ms.openlocfilehash: 1b5cef56cec30e5ad09500135e05884bf55d5dde
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076220"
---
# <a name="sql-modules"></a>SQL 모듈
SQL 문을 DBMS로 전송 하는 두 번째 방법은 모듈을 통하는 것입니다. 간단히 말해서 모듈은 호스트 프로그래밍 언어에서 호출 되는 프로시저 그룹으로 구성 됩니다. 각 프로시저에는 단일 SQL 문이 포함 되 고 데이터는 프로시저에서 매개 변수를 통해 전달 됩니다.  
  
 모듈은 응용 프로그램 코드에 연결 된 개체 라이브러리로 간주할 수 있습니다. 그러나 프로시저와 응용 프로그램의 나머지 부분을 연결 하는 방법은 구현에 따라 달라 집니다. 예를 들어 프로시저는 개체 코드로 컴파일되고 응용 프로그램 코드에 직접 연결 될 수 있으며, DBMS에서 컴파일되고 저장 되 고 응용 프로그램 코드에 배치 된 계획 식별자에 액세스 하기 위한 호출이 나 런타임에 해석 될 수 있습니다.  
  
 모듈의 주요 이점은 프로그래밍 언어에서 SQL 문을 완전히 분리 하는 것입니다. 이론적으로는 다른 항목을 변경 하지 않고 변경 하 여 다시 링크 하기만 하면 됩니다.
