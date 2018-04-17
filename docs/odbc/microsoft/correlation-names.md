---
title: 상관 관계 이름을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e3fd26a5b4601657d4f95ca629bc41666ef27309
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="correlation-names"></a>상관 관계 이름
상관 관계 이름은 완벽 하 게 지원 테이블 목록 내 포함 합니다. 예를 들어 다음 문자열 E1 Emp 라는 테이블에 대 한 상관 관계 이름입니다.  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```
