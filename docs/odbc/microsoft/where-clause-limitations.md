---
title: WHERE 조항 제한 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, WHERE clause limitations
- WHERE clause limitations [ODBC]
ms.assetid: 46b54f74-e4a3-4318-87cf-8a97c38a2718
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1699397db81d6fe702f60f6953fe7a0ae3726fe3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307564"
---
# <a name="where-clause-limitations"></a>WHERE 절 제한 사항
WHERE 절의 최대 절 수는 40입니다.  
  
 LONGVARBINARY 및 LONGVARCHAR 열은 길이가 최대 255자까지리터럴과 비교할 수 있지만 매개 변수를 사용하여 비교할 수는 없습니다.
