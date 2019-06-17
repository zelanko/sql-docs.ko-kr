---
title: SQLCloseCursor_ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 827f7195c5d4eb4f67cb3298b75519a5583053d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199506"
---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLCloseCursor** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLCloseCursor**를 참조 하십시오 [SQLCloseCursor 함수](../../../odbc/reference/syntax/sqlclosecursor-function.md)합니다.  
  
 커서 라이브러리 호출을 지원 하지 않습니다 **SQLCloseCursor** 열린 커서 없이 합니다. 이 시도 하는 SQLSTATE 24000 (잘못 된 커서 상태)를 반환 합니다. 호출 **SQLFreeStmt** 사용 하 여는 *옵션* SQL_CLOSE의 커서 라이브러리는 커서가 없습니다 열려 있습니다.
