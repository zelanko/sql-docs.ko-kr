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
ms.openlocfilehash: e82644d3bddab5d4f6fde6f7103bd9731872bab9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094195"
---
# <a name="default-driver-subkey"></a>기본 드라이버 하위 키
기본 하위 키에는 기본 데이터 원본에서 사용 하는 드라이버를 설명 하는 단일 값이 포함 됩니다. 이 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|data|  
|----------|---------------|----------|  
|**드라이버**|REG_SZ|*기본-드라이버-설명*|  
  
 *기본 드라이버 설명* 이름은 드라이버를 설명 하는 ODBC 드라이버 하위 키 아래에 있는 값의 이름과 동일 합니다.  
  
 예를 들어 기본 데이터 원본에서 SQL Server 드라이버를 사용 하는 경우 기본 하위 키의 값은 다음과 같을 수 있습니다.  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  기본 하위 키에 포함 된 기본 드라이버는 기본 사용자 DSN 또는 기본 시스템 DSN을 참조할 수 있습니다. 기본 사용자 DSN과 기본 시스템 DSN이 모두 생성 된 경우 기본 드라이버는 마지막으로 생성 된 DSN에 의해 결정 되므로 먼저 생성 된 DSN에 대 한 유효한 항목이 아닐 수 있습니다.
