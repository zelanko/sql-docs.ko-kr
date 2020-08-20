---
description: 상관 관계 이름
title: 상관 관계 이름 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24de7ec65b069839541cfa5cd272a221ebc96ecd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471645"
---
# <a name="correlation-names"></a>상관 관계 이름
상관 관계 이름은 테이블 목록을 포함 하 여 완전 하 게 지원 됩니다. 예를 들어 다음 문자열에서 E1은 Emp 라는 테이블의 상관 관계 이름입니다.  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```
