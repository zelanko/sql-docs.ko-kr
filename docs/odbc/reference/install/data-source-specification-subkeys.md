---
description: 데이터 소스 사양 하위 키
title: 데이터 원본 사양 하위 키 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8fabfd07779f74945bf647d20075de0cc057710b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494568"
---
# <a name="data-source-specification-subkeys"></a>데이터 소스 사양 하위 키
ODBC 데이터 원본 하위 키에 나열 된 각 데이터 원본에는 자체의 하위 키가 있습니다. 이 하위 키는 ODBC 데이터 원본 하위 키 아래에 있는 해당 값과 동일한 이름을 갖습니다. 이 하위 키의 값은 드라이버 DLL을 나열 하 고 데이터 원본에 대 한 설명을 나열할 수 있습니다. 드라이버가 번역기를 지 원하는 경우에는이 값에 기본 변환기의 이름, 기본 변환 DLL 및 기본 변환 옵션이 나열 될 수 있습니다. 값은 데이터 원본에 연결 하는 드라이버에 필요한 기타 정보를 나열할 수도 있습니다. 예를 들어 드라이버에는 서버 이름, 데이터베이스 이름 또는 스키마 이름이 필요할 수 있습니다.  
  
 값의 형식은 다음 표에 나와 있습니다. 드라이버 값만 필요 합니다.  
  
|Name|데이터 형식|데이터|  
|----------|---------------|----------|  
|Description|REG_SZ|*description*|  
|드라이버|REG_SZ|*드라이버 DLL-경로*|  
|TranslationDLL|REG_SZ|*translator-DLL 경로*|  
|TranslationName|REG_SZ|*번역기-이름*|  
|TranslationOption|REG_SZ|*번역-옵션*|  
|*opt-value-name*|*opt-값 형식*|*opt 값-데이터*|  
  
 예를 들어 SQL Server 드라이버에서 서버 이름과 ANSI 간 변환을 위한 플래그를 요구 하 고 이러한에 대 한 서버 및 OEMTOANSI 값을 정의 한다고 가정 합니다. 또한 인벤토리 데이터 원본에서 Microsoft® 코드 페이지 변환기를 사용 하 여 Windows® 라틴어 1 (1250) 및 다국어 (850) 코드 페이지 간을 변환 한다고 가정 합니다. 인벤토리 하위 키 아래에 있는 값은 다음과 같을 수 있습니다.  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
