---
title: "데이터 원본 사양 하위 키 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 61b485f55be504e894754f74c4ab779b9ebbaf5a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="data-source-specification-subkeys"></a>데이터 원본에 대 한 사양 하위 키
ODBC 데이터 소스 하위 키에 나열 된 각 데이터 원본 자체의 하위 키를 있습니다. 이 하위 키에 ODBC 데이터 원본 하위 키 아래에서 해당 값과 동일한 이름이 있습니다. 이 하위 키 아래 값 드라이버 DLL을 나열 해야 하 고 데이터 원본에 대 한 설명을 나열할 수 있습니다. 드라이버에서 변환기를 지 원하는 경우 기본 변환기, DLL, 기본 변환 및 기본 변환 옵션의 이름 값에 나열할 수 있습니다. 값은 데이터 원본에 연결 하는 드라이버에 필요한 기타 정보를 나열할 수 있습니다. 예를 들어, 드라이버는 서버 이름, 데이터베이스 이름 또는 스키마 이름이 필요할 수 있습니다.  
  
 다음 표에 표시 된은 값의 형식입니다. 드라이버 값만이 필요 합니다.  
  
|이름|데이터 형식|data|  
|----------|---------------|----------|  
|Description|REG_SZ|*설명*|  
|드라이버|REG_SZ|*드라이버 DLL 경로*|  
|TranslationDLL|REG_SZ|*변환기 DLL 경로*|  
|TranslationName|REG_SZ|*변환기 이름*|  
|TranslationOption|REG_SZ|*번역 옵션*|  
|*값 선택-이름*|*값 선택-형식*|*값 선택-데이터*|  
  
 예를 들어 SQL Server 드라이버가 OEM에 대 한 서버 이름 및 플래그를 ANSI 변환 하는 데 필요한 하 고 이러한 서버와 OEMTOANSI 값을 정의 합니다. 또한 인벤토리 데이터 원본은 Microsoft® 코드 페이지 변환기를 사용 하 여 Windows® 라틴어 1 (1250) 및 다국어 (850) 코드 페이지 간에 변환할 가정 합니다. 인벤토리 하위 키 아래에 값은 다음과 같을 수 있습니다.  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```

