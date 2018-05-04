---
title: SQLExtendedFetch (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4336f76093383a170fbb1028851564098213a74d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 2  
  
 비슷한 [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) 하지만 배열을 사용 하 여 각 열에 대해 여러 행을 반환 합니다. 결과 집합은 정방향 스크롤 가능 하 고 뒤로 스크롤할 수 있는 정적, 정방향 전용 커서가 정의 된 경우 만들 수 있습니다.  
  
 기본적으로 Visual FoxPro ODBC 드라이버는 FoxPro 테이블에서 삭제 된 것으로 표시 된 행을 반환 하지 않습니다. 삭제 하도록 표시 되었으나 아직 제거 되지 않은 테이블에서 행 결과 집합 커서에 포함 되지 않습니다. 사용 하 여이 동작을 변경할 수는 [삭제 설정](../../odbc/microsoft/set-deleted-command.md) 명령입니다.  
  
 자세한 내용은 참조 [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) 에 *ODBC Programmer's Reference*합니다.
