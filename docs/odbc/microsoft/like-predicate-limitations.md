---
title: 좋아요 조건자 제한 사항 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d596d688956d7bdbf3d9125184d81c16249781c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298963"
---
# <a name="like-predicate-limitations"></a>LIKE 조건자 제한 사항
열의 데이터가 255자보다 긴 경우 LIKE 비교는 처음 255자만 기준으로 합니다.  
  
 프로시저에 사용되는 LIKE는 상수 패턴으로만 지원됩니다. 데스크톱 데이터베이스 드라이버는 SQL-92 LIKE 패턴 일치를 지원합니다.  
  
 LIKE 조건자에서 이스케이프 절의 사용은 지원되지 않습니다.  
  
 숫자 또는 부동 데이터 형식의 데이터가 포함된 열에서는 LIKE 비교를 수행해서는 안 됩니다. 결과를 예측할 수 없습니다. 자세한 내용은 Microsoft *Jet 데이터베이스 엔진 프로그래머 가이드를*참조하십시오.
