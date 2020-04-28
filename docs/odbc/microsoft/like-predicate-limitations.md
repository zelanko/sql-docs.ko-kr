---
title: LIKE 조건자 제한 사항 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298963"
---
# <a name="like-predicate-limitations"></a>LIKE 조건자 제한 사항
열의 데이터가 255 자를 초과 하는 경우에는 첫 번째 255 문자만 기반으로 하는 비교를 사용할 수 있습니다.  
  
 프로시저에서 사용 되는 것은 상수 패턴 에서만 지원 됩니다. 데스크톱 데이터베이스 드라이버는 패턴 일치와 같은 SQL-92를 지원 합니다.  
  
 LIKE 조건자에는 escape 절을 사용할 수 없습니다.  
  
 Numeric 또는 float 데이터 형식의 데이터를 포함 하는 열에 대해서는 LIKE 비교를 수행 하면 안 됩니다. 결과를 예측할 수 없습니다. 자세한 내용은 *Microsoft Jet 데이터베이스 엔진 프로그래머 가이드*를 참조 하세요.
