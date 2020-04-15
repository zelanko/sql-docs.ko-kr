---
title: 커서 특성 매핑1 정보 유형 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d70cf0a93a6c6160faeb0afe991b2adfff11b8f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301046"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>커서 특성 1 정보 형식 매핑
때 ODBC 3. *x* 응용 프로그램은 SQL_XXXX_CURSOR_ATTRIBUTES1 정보 유형(동적, 정방향 전용, 키 집합 드라이버 또는 정적 커서의 경우)이 있는 ODBC*2.x* 드라이버에서 **SQLGetInfo를** 호출하며 드라이버 관리자에서 반환하는 비트의 설정은 ODBC 2에 따라 달라집니다. *x* 드라이버는 해당 ODBC 2에 대해 반환됩니다. *x* 정보 유형. 비트는 다음 표와 같이 설정됩니다.  
  
|비트 인<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|커서 유형|ODBC 2. *x* 정보<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|모두|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|동적, 키셋 드라이버, 정적|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|동적, 키셋 드라이버, 정적|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|모두|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|동적, 키셋 드라이버, 정적|SQL_POS_OPERATIONS|
