---
title: '4b 단계: 행 카운트 가져오기 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31ccbd15ae435165ea007fa9f3c0505c1dcc5aa0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302964"
---
# <a name="step-4b-fetch-the-row-count"></a>4b단계: 행 수 페치
다음 단계는 다음 그림과 같이 행 수를 가져오는 것입니다.  
  
 ![행의 수를 페치하는 방법](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 3 단계에서 실행 된 문이 **UPDATE**, **DELETE**또는 **INSERT** 문인 경우 응용 프로그램은 **SQLRowCount를**사용 하 여 영향을 받는 행의 수를 검색합니다. 자세한 내용은 [영향을 받는 행 수 확인을](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)참조하십시오.  
  
 이제 응용 프로그램은 3단계로 돌아와 동일한 트랜잭션에서 다른 문을 실행하거나 5단계로 이동하여 트랜잭션을 커밋하거나 롤백합니다.
