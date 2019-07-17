---
title: '4b단계: 행 수 페치 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9455c6589ed93a51e404f3e50d1cb86a0c0c8476
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114155"
---
# <a name="step-4b-fetch-the-row-count"></a>4b단계: 행 수 페치
다음 그림과에서 같이 행을 인출 하는 다음 단계가입니다.  
  
 ![행 수를 페치하는 방법](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 3 단계에서에서 실행 된 문의 경우는 **업데이트**를 **삭제**, 또는 **삽입** 문에서 응용 프로그램이 검색 된 영향을 받는 행의 수  **SQLRowCount**합니다. 자세한 내용은 [영향을 받는 행 개수 확인](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)합니다.  
  
 응용 프로그램에 이제 동일한 트랜잭션에서 다른 문을 실행 하는 3 단계로 반환 또는 커밋 또는 트랜잭션을 롤백하는 5 단계로 진행 됩니다.
