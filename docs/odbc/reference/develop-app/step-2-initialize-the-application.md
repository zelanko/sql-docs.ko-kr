---
description: '2단계: 애플리케이션 초기화'
title: '2 단계: 응용 프로그램 초기화 | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26d20a5b10ee7b414b9285a388359b3a93029f16
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482886"
---
# <a name="step-2-initialize-the-application"></a>2단계: 애플리케이션 초기화
두 번째 단계는 다음 그림에 표시 된 것 처럼 응용 프로그램을 초기화 하는 것입니다. 여기에서 수행 하는 작업은 응용 프로그램에 따라 다릅니다.  
  
 ![ODBC 응용 프로그램 초기화 방법](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 이 시점에서 **SQLGetInfo** 를 사용 하 여 드라이버의 기능을 검색 하는 것이 일반적입니다. 자세한 내용은 [사용할 데이터베이스 기능 고려](../../../odbc/reference/develop-app/considering-database-features-to-use.md)를 참조 하세요.  
  
 모든 응용 프로그램은 **SQLAllocHandle**를 사용 하 여 문 핸들을 할당 해야 하며 많은 응용 프로그램에서 커서 유형과 같은 문 특성을 **SQLSetStmtAttr**로 설정 합니다. 자세한 내용은 [문 핸들 할당](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) 및 [문 특성](../../../odbc/reference/develop-app/statement-attributes.md)을 참조 하세요.
