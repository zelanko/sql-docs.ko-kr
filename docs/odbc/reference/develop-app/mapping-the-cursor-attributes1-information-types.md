---
title: 커서 특성 1 정보 유형 매핑 | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036365"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>커서 특성 1 정보 형식 매핑
때 ODBC 3. *x* 응용 프로그램 호출 **SQLGetInfo** 는 ODBC 2 *.x* SQL_XXXX_CURSOR_ATTRIBUTES1 정보 형식 사용 하 여 드라이버 (동적, 정방향 전용, 키 집합-드라이버 또는 정적 커서의 경우) 드라이버 관리자에 의해 반환 된 비트 설정은 ODBC 2에 따라 달라 집니다. *x* 해당 하는 ODBC 2에 대 한 드라이버를 반환 합니다. *x* 정보 유형입니다. 다음 표에 나와 있는 것 처럼 해당 비트가 설정 됩니다.  
  
|비트<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|커서 유형|ODBC 2입니다. *x* 정보<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|All|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|동적으로 키 집합-드라이버, 정적|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|동적으로 키 집합-드라이버, 정적|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|All|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|동적으로 키 집합-드라이버, 정적|SQL_POS_OPERATIONS|
