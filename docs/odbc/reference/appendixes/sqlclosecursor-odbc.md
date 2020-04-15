---
title: SQLCloseCursor_ODBC | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1b61267d093e11bf7ea25158f5dc6a29ccba6a1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296303"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLCloseCursor** 함수의 사용에 대해 설명합니다. **SQLCloseCursor에**대한 일반 정보는 [SQLCloseCursor 함수를](../../../odbc/reference/syntax/sqlclosecursor-function.md)참조하십시오.  
  
 커서 라이브러리는 열린 커서없이 **SQLCloseCursor** 호출을 지원하지 않습니다. 이렇게 하면 SQLSTATE 24000(잘못된 커서 상태)이 반환됩니다. 커서가 열려 있지 않은 경우 SQL_CLOSE *옵션으로* **SQLFreeStmt를** 호출하는 것은 커서 라이브러리에서 지원됩니다.
