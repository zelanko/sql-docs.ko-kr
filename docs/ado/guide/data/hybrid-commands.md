---
description: 하이브리드 명령
title: 하이브리드 명령 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- hybrid commands [ADO]
- data shaping [ADO], hybrid commands
ms.assetid: e8ca40e8-459c-40e2-8dd3-3ec6d5ee7b51
author: rothja
ms.author: jroth
ms.openlocfilehash: fe4661618a56f208f0aeea7e66d5f57d4f95c44d
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805992"
---
# <a name="hybrid-commands"></a>하이브리드 명령
하이브리드 명령은 부분적으로 매개 변수가 있는 명령입니다. 예를 들면 다음과 같습니다.  
  
```  
SHAPE {select * from plants}   
   APPEND( {select * from customers where country = ?}   
           RELATE PlantCountry TO PARAMETER 0,   
             PlantRegion TO CustomerRegion )   
```  
  
 하이브리드 명령의 캐싱 동작은 일반적인 매개 변수가 있는 명령과 동일 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 셰이핑 예](./data-shaping-example.md)   
 [공식 모양 문법](./formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](./shape-commands-in-general.md)