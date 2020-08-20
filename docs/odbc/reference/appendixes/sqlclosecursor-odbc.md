---
description: SQLCloseCursor_ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d91ce573a48602ad6dce4f0cb0759c2c8dddd3aa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466055"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLCloseCursor** 함수를 사용 하는 방법을 설명 합니다. **SQLCloseCursor**에 대 한 일반 정보는 [SQLCloseCursor 함수](../../../odbc/reference/syntax/sqlclosecursor-function.md)를 참조 하세요.  
  
 커서 라이브러리는 열린 커서가 없는 **SQLCloseCursor** 호출을 지원 하지 않습니다. 이를 시도 하면 SQLSTATE 24000 (잘못 된 커서 상태)가 반환 됩니다. 커서가 열려 있지 않을 때 SQL_CLOSE *옵션* 을 사용 하 여 **SQLFreeStmt** 를 호출 하면 커서 라이브러리에서 지원 됩니다.
