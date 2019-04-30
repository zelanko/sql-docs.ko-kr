---
title: 기본 드라이버 하위 키 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default subkey [ODBC]
- registry entries for components [ODBC], default subkey
- subkeys [ODBC], default subkey
- drivers subkey [ODBC]
ms.assetid: 9e58b24f-ebfc-4286-a272-0843b4d6f2d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d78101fd564e18467e6833f480cec2409dc2c44b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198310"
---
# <a name="default-driver-subkey"></a>기본 드라이버 하위 키
기본 하위 키에는 기본 데이터 원본에서 사용 되는 드라이버를 설명 하는 단일 값을 포함 합니다. 이 값의 형식이 다음 표에 표시 됩니다.  
  
|이름|데이터 형식|data|  
|----------|---------------|----------|  
|**드라이버**|REG_SZ|*default-driver-description*|  
  
 합니다 *기본 드라이버 설명* 이름은 드라이버를 설명 하는 ODBC 드라이버 하위 키 아래 값의 이름과 동일 합니다.  
  
 예를 들어, 기본 데이터 원본 SQL Server 드라이버를 사용 하 여 기본 하위 키 아래에 값을 수 있습니다.  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  기본 하위 키에 포함 된 기본 드라이버는 기본 사용자 DSN 또는 기본 시스템 DSN 참조할 수 있습니다. 기본 사용자 DSN 및 기본 시스템 DSN을 만든 경우 기본 드라이버 먼저 생성 된 DSN에 유효한 항목이 없습니다 수 있으므로 마지막으로 생성 된 DSN으로 결정 됩니다.
