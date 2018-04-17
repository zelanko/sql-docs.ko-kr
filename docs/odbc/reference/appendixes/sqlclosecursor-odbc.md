---
title: SQLCloseCursor_ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9df09aea21ed6a1e7768dfd04ab283a8342d355
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLCloseCursor** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLCloseCursor**, 참조 [SQLCloseCursor 함수](../../../odbc/reference/syntax/sqlclosecursor-function.md)합니다.  
  
 커서 라이브러리가 호출을 지원 하지 않을 **SQLCloseCursor** 열린 커서 없이 합니다. 이 작업을 수행 SQLSTATE 24000 (잘못 된 커서 상태)를 반환 합니다. 호출 **SQLFreeStmt** 와 *옵션* SQL_CLOSE의 커서 라이브러리에서 지원 되는 없는 커서는 열려 있습니다.
