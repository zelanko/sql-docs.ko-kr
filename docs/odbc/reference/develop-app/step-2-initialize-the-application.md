---
title: '2단계: 응용 프로그램을 초기화 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41030015645bda11242a703a163f26104e66dba0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114245"
---
# <a name="step-2-initialize-the-application"></a>2단계: 애플리케이션 초기화
다음 그림에 나와 있는 것 처럼 응용 프로그램을 초기화 하는 두 번째 단계가입니다. 정확 하 게 수행 되는 다음 응용 프로그램을 사용 하 여 달라 집니다.  
  
 ![ODBC 응용 프로그램 초기화를 보여 줍니다](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 이 시점에서 일반적으로 사용 하는 **SQLGetInfo** 드라이버의 기능을 검색 합니다. 자세한 내용은 [사용할 데이터베이스 기능 고려](../../../odbc/reference/develop-app/considering-database-features-to-use.md)합니다.  
  
 모든 응용 프로그램을 사용 하 여 문 핸들을 할당 해야 **SQLAllocHandle**, 및 대부분의 응용 프로그램 집합 커서 유형과 같이 문 특성 **SQLSetStmtAttr**합니다. 자세한 내용은 [문 핸들 할당](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) 하 고 [문 특성](../../../odbc/reference/develop-app/statement-attributes.md)합니다.
