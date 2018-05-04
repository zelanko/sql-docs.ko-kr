---
title: SQLGetInfo (커서 라이브러리) | Microsoft Docs
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
- SQLGetInfo function [ODBC], Cursor Library
ms.assetid: 1b4d220d-2c07-4f56-987e-36813bb1a6ce
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c8a3cfcc70ddb26403b73895d71cafc923b8a655
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetinfo-cursor-library"></a>SQLGetInfo (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLGetInfo** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLGetInfo**, 참조 [SQLGetInfo 함수](../../../odbc/reference/syntax/sqlgetinfo-function.md)합니다.  
  
 커서 라이브러리의 다음 값에 대 한 값을 반환 합니다. *정보 항목* (&#124; 비트 OR 연산자를 나타내는)의 다른 모든 값에 대 한; *정보 항목*, 호출 **SQLGetInfo** 드라이버입니다.  
  
|*정보 항목*|반환 값|  
|----------------|--------------------|  
|SQL_BOOKMARK_PERSISTENCE|SQL_BP_SCROLL|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|0|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|0|  
|SQL_FETCH_DIRECTION [1]|SQL_FD_FETCH_ABSOLUTE &AMP;#124; SQL_FD_FETCH_FIRST &AMP;#124; SQL_FD_FETCH_LAST &AMP;#124; SQL_FD_FETCH_NEXT &AMP;#124; SQL_FD_FETCH_PRIOR &AMP;#124; SQL_FD_FETCH_RELATIVE &AMP;#124; SQL_FD_FETCH_BOOKMARK|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT &AMP;#124; SQL_CA1_ABSOLUTE &AMP;#124; SQL_CA1_RELATIVE &AMP;#124; SQL_CA1_LOCK_NO_CHANGE &AMP;#124; SQL_CA1_POS_POSITION &AMP;#124; SQL_CA1_POSITIONED_DELETE &AMP;#124; SQL_CA1_POSITIONED_UPDATE &AMP;#124; SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &AMP;#124; SQL_CA2_OPT_VALUES_CONCURRENCY &AMP;#124; SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_GETDATA_EXTENSIONS|SQL_GD_BLOCK &#124; 드라이버에서 반환 된 값 **참고:** 와 데이터를 검색 하는 경우 **SQLFetchScroll**, **SQLGetData** 지정 된 기능을 지원 합니다. SQL_GD_ANY_COLUMN 및 SQL_GD_BOUND 마스크로 합니다.|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES1|0|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES2|0|  
|SQL_LOCK_TYPES [1]|SQL_LCK_NO_CHANGE|  
|SQL_STATIC_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT &AMP;#124; SQL_CA1_ABSOLUTE &AMP;#124; SQL_CA1_RELATIVE &AMP;#124; SQL_CA1_BOOKMARK &AMP;#124; SQL_CA1_LOCK_NO_CHANGE &AMP;#124; SQL_CA1_POS_POSITION &AMP;#124; SQL_CA1_POSITIONED_DELETE &AMP;#124; SQL_CA1_POSITIONED_UPDATE &AMP;#124; SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_STATIC_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &AMP;#124; SQL_CA2_OPT_VALUES_ 동시성 &AMP;#124; SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_POS_OPERATIONS [1]|SQL_POS_POSITION|  
|SQL_POSITIONED_STATEMENTS [1]|SQL_PS_POSITIONED_DELETE &AMP;#124; SQL_PS_POSITIONED_UPDATE &AMP;#124; SQL_PS_SELECT_FOR_UPDATE|  
|SQL_ROW_UPDATES|"Y"|  
|SQL_SCROLL_CONCURRENCY [1]|SQL_SCCO_READ_ONLY &AMP;#124; SQL_SCCO_OPT_VALUES|  
|SQL_SCROLL_OPTIONS|SQL_SO_FORWARD_ONLY &AMP;#124; SQL_SO_STATIC|  
|SQL_STATIC_SENSITIVITY [1]|SQL_SS_UPDATES|  
  
 [1] ODBC 2.x 드라이버 커서 라이브러리를 사용할 때만 사용 합니다.  
  
> [!IMPORTANT]  
>  트랜잭션이 커밋 또는 데이터 원본으로 롤백할 때 커서 라이브러리 같은 커서 동작을 구현 합니다. 즉, 커밋 또는 호출 하 여 트랜잭션을 롤백하면 **SQLEndTran** SQL_ATTR_AUTOCOMMIT 연결 특성을 사용 하면이 데이터 원본에 대 한 액세스 계획을 삭제 하 고 모든 문에 대해 커서를 닫습니다 하거나 연결을 사용 합니다. 자세한 내용은 참조에서 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 유형이 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)합니다.
