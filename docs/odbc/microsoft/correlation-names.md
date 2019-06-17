---
title: 상관 관계 이름을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b8a253f9d252beb42080d2085adb962206ebd94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232315"
---
# <a name="correlation-names"></a>상관 관계 이름
상관 관계 이름은 완전히 지원 테이블 목록에 포함 합니다. 예를 들어 다음 문자열에 E1 되 Emp 라는 테이블에 대 한 상관 관계 이름입니다.  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```
