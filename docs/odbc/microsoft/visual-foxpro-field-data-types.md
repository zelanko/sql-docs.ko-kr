---
description: Visual FoxPro 필드 데이터 형식
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
ms.openlocfilehash: 65410f16367af8764e8572c58e53831f3f7b9cda
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449055"
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
|L|-|-|논리적|  
|M|-|-|메모|  
|N|N|d|소수 자릿수가 *d* 인 너비 *n* 의 숫자 필드|  
|T|-|-|DateTime|  
|Y|-|-|통화|
