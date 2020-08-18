---
description: 데이터 형식 제한 사항
title: 데이터 형식 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4853846f21aa0ad763295bbdc4233c472ac53864
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412789"
---
# <a name="data-type-limitations"></a>데이터 형식 제한 사항
Microsoft ODBC Desktop Database 드라이버는 데이터 형식에 대해 다음과 같은 제한 사항을 적용 합니다.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|모든 데이터 형식|형식 변환 실패로 인해 영향을 받는 열이 NULL로 설정 될 수 있습니다.|  
|BINARY|길이가 0 인 이진 열을 만들면 실제로 255 바이트 이진 열이 반환 됩니다.|  
|DATE|DATE 데이터 형식을 CONVERT 함수에서 다른 데이터 형식 (또는 자체)으로 변환할 수 없습니다.|  
|DECIMAL (정확한 숫자)|지원되지 않습니다.|  
|부동 소수점 데이터 형식|부동 소수점 숫자의 소수 자릿수는 Windows 제어판의 국가별 섹션에 설정 된 숫자 형식에 따라 제한 될 수 있습니다.|  
|NUMERIC|최대 전체 자릿수와 28의 소수 자릿수를 지원 합니다.|  
|timestamp|TIMESTAMP 데이터 형식은 CONVERT 함수에 의해 자기 자신으로 변환할 수 없습니다.|  
|TINYINT|TINYINT 값은 항상 부호가 없습니다.|  
|길이가 0 인 문자열|DBASE, Microsoft Excel, Paradox 또는 Textdriver를 사용 하는 경우 열에 길이가 0 인 문자열을 삽입 하면 실제로 NULL이 삽입 됩니다.|
