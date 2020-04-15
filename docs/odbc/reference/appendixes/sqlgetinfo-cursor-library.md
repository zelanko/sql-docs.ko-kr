---
title: SQLGetInfo (커서 라이브러리) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Cursor Library
ms.assetid: 1b4d220d-2c07-4f56-987e-36813bb1a6ce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9067fd8b33cb2408f1ef6f0e58603eb4f1f7eb09
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307814"
---
# <a name="sqlgetinfo-cursor-library"></a>SQLGetInfo(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLGetInfo** 함수의 사용에 대해 설명합니다. **SQLGetInfo에**대한 일반 정보는 [SQLGetInfo 함수를](../../../odbc/reference/syntax/sqlgetinfo-function.md)참조하십시오.  
  
 커서 라이브러리는 *InfoType(&#124;비트* OR를 나타내기 위해 다음 값에 대한 값을 반환합니다. *InfoType의*다른 모든 값에 대 한 드라이버에서 **SQLGetInfo를** 호출 합니다.  
  
|*정보 입력*|반환 값|  
|----------------|--------------------|  
|SQL_BOOKMARK_PERSISTENCE|SQL_BP_SCROLL|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|0|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|0|  
|SQL_FETCH_DIRECTION[1]|SQL_FD_FETCH_ABSOLUTE &#124; SQL_FD_FETCH_FIRST &#124; SQL_FD_FETCH_LAST &#124; SQL_FD_FETCH_NEXT &#124; SQL_FD_FETCH_PRIOR &#124; SQL_FD_FETCH_RELATIVE &#124; SQL_FD_FETCH_BOOKMARK|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_RELATIVE &#124; &#124; SQL_CA1_NEXT SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_UPDATE &#124; SQL_CA1_POS_POSITION SQL_CA1_POS_POSITION &#124; SQL_CA1_ABSOLUTE SQL_CA1_ABSOLUTE SQL_CA1_ABSOLUTE SQL_CA1_ABSOLUTE SQL_CA1_ABSOLUTE SQL_CA1_ABSOLUTE SQL_CA1_ABSOLUTE SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_UPDATE SQL_CA1_POS_POSITION SQL_CA1_LOCK_NO_CHANGE SQL_CA1_SELECT_FOR_UPDATE &#124; SQL_CA1_POSITIONED_DELETE &#124; &#124; &#124;.|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &#124; SQL_CA2_OPT_VALUES_CONCURRENCY &#124; SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_GETDATA_EXTENSIONS|SQL_GD_BLOCK &#124; 드라이버에서 반환되는 값 **참고:** **SQLFetchScroll로**데이터를 검색할 때 **SQLGetData는** SQL_GD_ANY_COLUMN 및 SQL_GD_BOUND 비트마스크로 지정된 기능을 지원합니다.|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES1|0|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES2|0|  
|SQL_LOCK_TYPES[1]|SQL_LCK_NO_CHANGE|  
|SQL_STATIC_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT &#124; SQL_CA1_ABSOLUTE &#124; SQL_CA1_RELATIVE &#124; SQL_CA1_BOOKMARK &#124; SQL_CA1_LOCK_NO_CHANGE &#124; SQL_CA1_POS_POSITION &#124; SQL_CA1_POSITIONED_DELETE &#124; SQL_CA1_POSITIONED_UPDATE &#124; SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_STATIC_CURSOR_ATTRIBUTES2|&#124; SQL_CA2_READ_ONLY_CONCUR SQL_CA2_OPT_VALUES_ SQL_CA2_OPT_VALUES_ SQL_CA2_SENSITIVITY_UPDATES &#124;.|  
|SQL_POS_OPERATIONS[1]|SQL_POS_POSITION|  
|SQL_POSITIONED_STATEMENTS[1]|SQL_PS_POSITIONED_DELETE &#124; SQL_PS_POSITIONED_UPDATE &#124; SQL_PS_SELECT_FOR_UPDATE|  
|SQL_ROW_UPDATES|"Y"|  
|SQL_SCROLL_CONCURRENCY[1]|SQL_SCCO_READ_ONLY &#124; SQL_SCCO_OPT_VALUES|  
|SQL_SCROLL_OPTIONS|SQL_SO_FORWARD_ONLY &#124; SQL_SO_STATIC|  
|SQL_STATIC_SENSITIVITY[1]|SQL_SS_UPDATES|  
  
 [1] ODBC 2.x 드라이버와 함께 커서 라이브러리를 사용하는 경우에만 사용됩니다.  
  
> [!IMPORTANT]  
>  커서 라이브러리는 트랜잭션이 데이터 원본으로 커밋되거나 롤백될 때 동일한 커서 동작을 구현합니다. 즉, **SQLEndTran을** 호출하거나 SQL_ATTR_AUTOCOMMIT 연결 특성을 사용하여 트랜잭션을 커밋하거나 롤백하면 데이터 원본이 액세스 계획을 삭제하고 연결의 모든 명령문에 대한 커서를 닫을 수 있습니다. 자세한 내용은 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 정보 형식을 [참조하십시오.](../../../odbc/reference/syntax/sqlgetinfo-function.md)
