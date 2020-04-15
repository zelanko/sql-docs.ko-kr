---
title: 데이터 소스 사양 하위 키 | 마이크로 소프트 문서
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
ms.openlocfilehash: 281377c307f3f3750e87bf5dc988beb7660067af
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300343"
---
# <a name="data-source-specification-subkeys"></a>데이터 소스 사양 하위 키
ODBC 데이터 원본 하위 키에 나열된 각 데이터 원본에는 자체 하위 키가 있습니다. 이 하위 키의 이름은 ODBC 데이터 원본 하위 키 아래의 해당 값과 동일합니다. 이 하위 키 아래의 값은 드라이버 DLL을 나열해야 하며 데이터 원본에 대한 설명을 나열할 수 있습니다. 드라이버가 번역기를 지원하는 경우 값에는 기본 번역기이름, 기본 번역 DLL 및 기본 번역 옵션이 나열될 수 있습니다. 이 값은 드라이버가 데이터 원본에 연결하는 데 필요한 다른 정보를 나열할 수도 있습니다. 예를 들어 드라이버에 서버 이름, 데이터베이스 이름 또는 스키마 이름이 필요할 수 있습니다.  
  
 값의 형식은 다음 표에 나와 있습니다. 드라이버 값만 필요합니다.  
  
|속성|데이터 형식|데이터|  
|----------|---------------|----------|  
|설명|REG_SZ|*설명*|  
|드라이버|REG_SZ|*드라이버 DLL 경로*|  
|번역DLL|REG_SZ|*번역기-DLL 경로*|  
|번역 이름|REG_SZ|*번역자 이름*|  
|번역 옵션|REG_SZ|*번역 옵션*|  
|*옵트-값 이름*|*옵트-값 유형*|*옵트-가치-데이터*|  
  
 예를 들어 SQL Server 드라이버에 ANSI 변환에 대한 OEM에 대한 서버 이름과 플래그가 필요하고 이러한 값에 대한 서버 및 OEMTOANSI 값을 정의한다고 가정합니다. 또한 인벤토리 데이터 원본이 Microsoft® 코드 페이지 번역기를 사용하여 Windows® 라틴어 1(1250) 및 다국어(850) 코드 페이지 간에 번역한다고 가정합니다. 인벤토리 하위 키 아래의 값은 다음과 같습니다.  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
