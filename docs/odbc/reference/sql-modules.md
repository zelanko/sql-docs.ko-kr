---
title: SQL 모듈 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 351d1c6a34413b385bd76dfebb009b34c4c0f150
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280430"
---
# <a name="sql-modules"></a>SQL 모듈
DBMS에 SQL 문을 보내는 두 번째 방법은 모듈을 통해서입니다. 간단히 말해서 모듈은 호스트 프로그래밍 언어에서 호출되는 프로시저 그룹으로 구성됩니다. 각 프로시저에는 단일 SQL 문이 포함되며 데이터는 프로시저에서 매개 변수를 통해 전달됩니다.  
  
 모듈은 응용 프로그램 코드에 연결된 개체 라이브러리로 생각할 수 있습니다. 그러나 프로시저와 응용 프로그램의 나머지 부분을 연결하는 정확한 방법은 구현에 따라 다릅니다. 예를 들어 프로시저를 개체 코드로 컴파일하고 응용 프로그램 코드에 직접 연결할 수 있으며, DBMS에 컴파일 및 저장되고 응용 프로그램 코드에 배치된 계획 식별자에 액세스하기 위한 호출을 호출하거나 런타임에 해석될 수 있습니다.  
  
 모듈의 주요 장점은 프로그래밍 언어에서 SQL 문을 깔끔하게 분리한다는 것입니다. 이론적으로는 다른 것을 변경하지 않고 하나를 변경하고 단순히 다시 연결할 수 있어야합니다.
