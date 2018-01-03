---
title: "Visual FoxPro 필드 데이터 형식 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c99a094c690882c6f2877964ae19b335cff1509
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 필드 데이터 형식
다음 표에서에 대 한 값을 보여 줍니다.는 *FieldType* ALTER TABLE 및 CREATE TABLE에서 인수를 나타내고 여부 *nFieldWidth* 및 *nPrecision* 인수는 필수.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|너비의 문자 필드*n*|  
|d|-|-|date|  
|F|N|d|숫자 필드의 너비를 부동  *n*  와 *d* 소수 자릿수|  
|G|-|-|일반|  
|I|-|-|정수|  
|L|-|-|논리|  
|M|-|-|메모|  
|N|N|d|숫자 필드 너비의  *n*  와 *d* 소수 자릿수|  
|T|-|-|DateTime|  
|Y|-|-|Currency|
