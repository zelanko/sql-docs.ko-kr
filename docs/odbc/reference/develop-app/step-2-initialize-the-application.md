---
title: '2단계: 응용 프로그램 초기화 | 마이크로 소프트 문서'
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
ms.openlocfilehash: 843155ba6b641ea26717e63af55c8774f963a800
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288269"
---
# <a name="step-2-initialize-the-application"></a>2단계: 애플리케이션 초기화
두 번째 단계는 다음 그림과 같이 응용 프로그램을 초기화하는 것입니다. 여기서 수행되는 작업은 응용 프로그램에 따라 다릅니다.  
  
 ![ODBC 응용 프로그램 초기화 방법](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 이 시점에서 **SQLGetInfo를** 사용하여 드라이버의 기능을 검색하는 것이 일반적입니다. 자세한 내용은 [사용할 데이터베이스 기능 고려를](../../../odbc/reference/develop-app/considering-database-features-to-use.md)참조하십시오.  
  
 모든 응용 프로그램은 **SQLAllocHandle을**사용하여 문 핸들을 할당해야 하며 많은 응용 프로그램은 **SQLSetStmtAttr**을 사용하여 커서 유형과 같은 문 특성을 설정합니다. 자세한 내용은 [명령문 핸들](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) 및 [명령문 특성 할당을](../../../odbc/reference/develop-app/statement-attributes.md)참조하십시오.
