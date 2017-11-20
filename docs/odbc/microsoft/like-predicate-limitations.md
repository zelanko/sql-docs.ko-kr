---
title: "제한 사항 조건자와 같은 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5668f03e785c0d27133965f16af40ce69c2a2567
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="like-predicate-limitations"></a>마찬가지로 조건자 제한 사항
데이터 열에 255 자 보다 긴 경우 LIKE 비교가에서는 처음 255 자만에 대해서만 기반 합니다.  
  
 LIKE에서 사용 되는 프로시저 상수 패턴에만 지원 됩니다. 데스크톱 데이터베이스 드라이버와 같은 SQL 92 패턴 일치를 지원합니다.  
  
 LIKE 조건자에서 escape 절 사용은 지원 되지 않습니다.  
  
 LIKE 비교를 숫자 또는 float 데이터 형식의 데이터를 포함 하는 열에서 수행 되어야 합니다. 결과 예측할 수 있습니다. 자세한 내용은 참조는 *Microsoft Jet 데이터베이스 엔진 Programmer's Guide*합니다.

