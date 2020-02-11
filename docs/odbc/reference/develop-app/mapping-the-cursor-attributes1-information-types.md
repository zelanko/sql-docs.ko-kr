---
title: 커서 Attributes1 정보 형식 매핑 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d95d3e67fdcd7159074e2f20ffa558f4c80bbcb2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036365"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>커서 특성 1 정보 형식 매핑
ODBC 3 인 경우 *x* 응용 프로그램은 SQL_XXXX_CURSOR_ATTRIBUTES1 정보 유형을 사용 하 여 odbc 2.x 드라이버에서 **SQLGetInfo** 를 호출 합니다 (동적, 전방 전용, 키 집합-드라이버 또는 정적 커서의 경우 *). 드라이버* 관리자에서 반환 된 비트의 설정은 odbc 2에 따라 다릅니다. *x* 드라이버는 해당 ODBC 2에 대해를 반환 합니다. *x* 정보 유형입니다. 비트는 다음 표와 같이 설정 됩니다.  
  
|비트<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|커서 유형|ODBC 2. *x* 정보<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|모두|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|동적, 키 집합-드라이버, 정적|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|동적, 키 집합-드라이버, 정적|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|모두|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|동적, 키 집합-드라이버, 정적|SQL_POS_OPERATIONS|
