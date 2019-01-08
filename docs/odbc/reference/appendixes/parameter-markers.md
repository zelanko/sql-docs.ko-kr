---
title: 매개 변수 표식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 833e2740e54f07701fb66a894bb5e4798c4a42e2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516396"
---
# <a name="parameter-markers"></a>매개 변수 표식
SQL-92 사양에 따라 응용 프로그램은 다음 위치에 매개 변수 표식을 배치할 수 없습니다. 보다 포괄적인 목록은 SQL-92 사양을 참조 하세요.  
  
-   에 **선택** 목록  
  
-   둘 다로 *식을* 에 *비교 조건자*  
  
-   이항 연산자의 피연산자가 모두로  
  
-   첫 번째와 두 번째 피연산자가 모두의는 **BETWEEN** 작업  
  
-   첫 번째 및 세 번째 피연산자로 **BETWEEN** 작업  
  
-   식 및 첫 번째 값을 **IN** 작업  
  
-   단항 피연산자로 + 또는-작업  
  
-   함수의 인수로 *집합 함수 참조*  
  
 매개 변수 표식에 대 한 자세한 내용은 SQL-92 사양을 참조 하세요. 매개 변수에 대 한 자세한 내용은 참조 하십시오 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다.
