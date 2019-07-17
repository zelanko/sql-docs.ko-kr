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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8cd3cebfcf20df2f8a3a786ea66fd28dd76307c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119706"
---
# <a name="like-predicate-limitations"></a>LIKE 조건자 제한 사항
데이터 열에 255 자 보다 긴 경우에서는 처음 255 자만 에서만 LIKE 비교에 따라 달라 집니다.  
  
 ' 좋아요 '를 사용 하는 프로시저 상수 패턴 에서만 지원 됩니다. 데스크톱 데이터베이스 드라이버와 같은 SQL-92 패턴 일치를 지원합니다.  
  
 LIKE 조건자에 이스케이프 절을 사용 하 여 지원 되지 않습니다.  
  
 LIKE 비교를 숫자 또는 float 데이터 형식의 데이터를 포함 하는 열에서 수행 되어야 합니다. 결과 예측할 수 없습니다. 자세한 내용은 참조는 *Microsoft Jet 데이터베이스 엔진 Programmer's Guide*합니다.
