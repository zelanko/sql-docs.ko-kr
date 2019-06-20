---
title: 데이터 소스 사양 하위 키 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad210f91d00f9e692c8ee20fef01a808a01501c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198213"
---
# <a name="data-source-specification-subkeys"></a>데이터 소스 사양 하위 키
ODBC 데이터 원본 하위 키에 나열 된 각 데이터 원본에는 자체의 하위 키를 있습니다. 이 하위 키는 ODBC 데이터 원본 하위 키 아래에서 해당 값으로 동일한 이름이 있습니다. 이 하위 키 아래의 값 드라이버 DLL을 나열 해야 및 데이터 원본에 대 한 설명을 나열할 수 있습니다. 드라이버에서 번역을 지 원하는 경우 값을 기본 변환기, DLL, 기본 변환 및 기본 변환 옵션 이름을 나열할 수 있습니다. 값은 드라이버에서 데이터 원본에 연결 하는 데 필요한 기타 정보를 나열할 수도 있습니다. 예를 들어, 서버 이름, 데이터베이스 이름 또는 스키마 이름 드라이버가 필요할 수 있습니다.  
  
 값의 형식은 다음 표에 나와 있는 것 처럼입니다. 만 드라이버 값이 필요 합니다.  
  
|이름|데이터 형식|data|  
|----------|---------------|----------|  
|Description|REG_SZ|*description*|  
|드라이버|REG_SZ|*driver-DLL-path*|  
|TranslationDLL|REG_SZ|*translator-DLL-path*|  
|TranslationName|REG_SZ|*translator-name*|  
|TranslationOption|REG_SZ|*translation-option*|  
|*opt-value-name*|*opt-value-type*|*opt-value-data*|  
  
 예를 들어 SQL Server 드라이버 OEM에 대 한 서버 이름과 플래그를 ANSI 변환 하는 데 필요한 하 고 이러한 서버 및 OEMTOANSI 값을 정의 합니다. 또한 Microsoft® 코드 페이지 Translator를 사용 하 여 Windows® 라틴어 1 (1250) 및 다국어 (850) 코드 페이지 사이 변환 인벤토리 데이터 소스는 가정 합니다. 인벤토리 하위 키 아래의 값은 다음과 같을 수 있습니다.  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
