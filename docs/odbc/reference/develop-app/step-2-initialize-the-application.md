---
title: "2 단계: 응용 프로그램을 초기화 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4b14b5374cedece38295bac840a72acae5895ca8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="step-2-initialize-the-application"></a>2 단계: 응용 프로그램 초기화
다음 그림에 나와 있는 것 처럼 응용 프로그램을 초기화 하는 두 번째 단계가입니다. 정확 하 게 수행 되는 동작과 여기 응용 프로그램에 따라 달라 집니다.  
  
 ![ODBC 응용 프로그램 초기화를 보여 줍니다.](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 이 시점에서 일반적으로 사용 하는 **SQLGetInfo** 드라이버의 기능을 검색 합니다. 자세한 내용은 참조 [데이터베이스 기능 사용을 고려](../../../odbc/reference/develop-app/considering-database-features-to-use.md)합니다.  
  
 모든 응용 프로그램으로 문 핸들을 할당 해야 할 **SQLAllocHandle**, 대부분의 응용 프로그램 사용 하 여 커서 유형과 같이 문 특성을 설정할 **SQLSetStmtAttr**합니다. 자세한 내용은 참조 [문 핸들 할당](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) 및 [문 특성](../../../odbc/reference/develop-app/statement-attributes.md)합니다.
