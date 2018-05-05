---
title: 드라이버의 하위 키를 기본 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default subkey [ODBC]
- registry entries for components [ODBC], default subkey
- subkeys [ODBC], default subkey
- drivers subkey [ODBC]
ms.assetid: 9e58b24f-ebfc-4286-a272-0843b4d6f2d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6563627087ce8516f74f478b35f0f6a896aa025b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="default-driver-subkey"></a>기본 드라이버의 하위 키
기본 하위 키에서 기본 데이터 원본을 사용 하는 드라이버를 설명 하는 단일 값을 포함 합니다. 이 값의 형식은 다음 표에 표시 됩니다.  
  
|이름|데이터 형식|Data|  
|----------|---------------|----------|  
|**드라이버**|REG_SZ|*기본 드라이버-설명*|  
  
 *기본 드라이버 설명* 이름은 드라이버에 설명 하는 ODBC 드라이버 하위 키 아래에 있는 값의 이름으로 동일 합니다.  
  
 예를 들어 기본 데이터 원본은 SQL Server 드라이버를 사용 하 여 기본 하위 키 아래에 있는 값 수 있습니다.  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  기본 하위 키에 포함 된 기본 드라이버는 기본 사용자 DSN 또는 기본 시스템 DSN 참조할 수 있습니다. 기본 사용자 DSN와 기본 시스템 DSN을 만든 경우 기본 드라이버 때문에 처음 생성 된 DSN에 유효한 항목이 아닐 수 마지막으로, 생성 된 DSN으로 결정 됩니다.
