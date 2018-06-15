---
title: '4b 단계: 행 개수를 반입 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b90259758ceab600abce600bdfdab6edc52f506
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915258"
---
# <a name="step-4b-fetch-the-row-count"></a>4b 단계: 인출 된 행 수
다음 단계는 다음 그림에 나와 있는 것 처럼 인출할 행 수입니다.  
  
 ![행 개수를 페치하](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 3 단계에서에서 실행 된 문의 경우는 **업데이트**, **삭제**, 또는 **삽입** 문, 응용 프로그램으로 영향을 받는 행의 수를 검색  **SQLRowCount**합니다. 자세한 내용은 참조 [영향을 받는 행 개수 확인](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)합니다.  
  
 응용 프로그램은 이제 동일한 트랜잭션 내에서 다른 문을 실행 하는 3 단계를 반환 하거나 트랜잭션을 커밋하거나 5 단계로 진행 됩니다.
