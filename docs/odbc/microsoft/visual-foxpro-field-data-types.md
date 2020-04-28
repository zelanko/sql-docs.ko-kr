---
title: Visual FoxPro 필드 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72313e0269c93bca9cb2561d89604c3c88c8567b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304804"
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 필드 데이터 형식
다음 표에서는 ALTER TABLE 및 CREATE TABLE의 *FieldType* 인수 값을 나열 하 고 *Nfieldwidth* 및 *nprecision* 인수가 필요한 지 여부를 나타냅니다.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|설명|  
|-----------------|-------------------|------------------|-----------------|  
|b|-|d|Double|  
|C|N|-|너비 *n* 의 문자 필드|  
|D|-|-|Date|  
|F|N|d|소수 자릿수가 *d* 인 너비 *n* 의 부동 숫자 필드|  
|G|-|-|일반|  
|I|-|-|정수|  
|L|-|-|논리|  
|M|-|-|메모|  
|N|N|d|소수 자릿수가 *d* 인 너비 *n* 의 숫자 필드|  
|T|-|-|DateTime|  
|Y|-|-|Currency|
