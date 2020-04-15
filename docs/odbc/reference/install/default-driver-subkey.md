---
title: 기본 드라이버 하위 키 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb134d670964e352d94c13474d8a72fa4bd494ba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301056"
---
# <a name="default-driver-subkey"></a>기본 드라이버 하위 키
기본 하위 키에는 기본 데이터 원본에서 사용하는 드라이버를 설명하는 단일 값이 포함되어 있습니다. 이 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|데이터|  
|----------|---------------|----------|  
|**드라이버**|REG_SZ|*기본 드라이버 설명*|  
  
 *기본 드라이버 설명* 이름은 드라이버를 설명하는 ODBC 드라이버 하위 키 아래의 값 이름과 동일합니다.  
  
 예를 들어 기본 데이터 원본에서 SQL Server 드라이버를 사용하는 경우 기본 하위 키 아래의 값은 다음과 같은 값일 수 있습니다.  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  기본 하위 키에 포함된 기본 드라이버는 기본 사용자 DSN 또는 기본 시스템 DSN을 참조할 수 있습니다. 기본 사용자 DSN과 기본 시스템 DSN이 모두 생성된 경우 기본 드라이버는 마지막으로 만든 DSN에 의해 결정되므로 먼저 만들어진 DSN에 대한 유효한 항목이 아닐 수 있습니다.
