---
title: 비주얼 폭스프로 필드 데이터 유형 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304804"
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro 필드 데이터 형식
다음 표는 ALTER TABLE 및 CREATE TABLE에서 *FieldType* 인수에 대한 값을 나열하고 *nFieldWidth* 및 *nPrecision* 인수가 필요한지 여부를 나타냅니다.  
  
|*필드 타입*|*N필드 폭*|*n정밀도*|설명|  
|-----------------|-------------------|------------------|-----------------|  
|b|-|d|Double|  
|C|N|-|*너비* n의 문자 필드|  
|D|-|-|Date|  
|F|N|d|*d* 소수 자릿수가 있는 너비 *n의* 부동 숫자 필드|  
|G|-|-|일반|  
|I|-|-|정수|  
|L|-|-|논리|  
|M|-|-|메모|  
|N|N|d|*d* 소수 자릿수가 있는 너비 *n의* 숫자 필드|  
|T|-|-|DateTime|  
|Y|-|-|통화|
