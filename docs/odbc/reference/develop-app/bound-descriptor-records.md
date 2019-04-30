---
title: 바인딩된 설명자 레코드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f7d21a1166868603f9389ab4ef5c5b3448b0312
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199524"
---
# <a name="bound-descriptor-records"></a>바인딩된 설명자 레코드
Null 값을 더 이상 포함 되도록 설명자 레코드의 SQL_DESC_DATA_PTR 필드가 설정 하는 응용 프로그램, 레코드 라고 *바인딩된*합니다.  
  
 설명자는 APD 이면 바인딩된 각 레코드는 바인딩된 매개 변수를 구성 합니다. 입력된 매개 변수에 대 한 응용 프로그램은 문을 실행 하기 전에 SQL 문에서 각 동적 매개 변수 표식에 대 한 매개 변수를 바인딩해야 합니다. 출력 매개 변수에 대 한 응용 프로그램 매개 변수를 바인딩하지 필요 합니다.  
  
 설명자는 카드가 데이터베이스 데이터의 행을 설명 하는 경우 바인딩된 각 레코드는 바인딩된 열을 구성 합니다.
