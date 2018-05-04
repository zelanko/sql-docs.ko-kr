---
title: SQLFreeStmt (커서 라이브러리) | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2cd1e2eef830ef36887f488dcd6f6c0f4aac0483
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLFreeStmt** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLFreeStmt**, 참조 [SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)합니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLFreeStmt** 호출한 후 SQL_UNBIND 옵션과 함께 **SQLExtendedFetch**, **SQLFetch**, 또는 **SQLFetchScroll**, 커서 라이브러리는 오류를 반환 합니다. 결과 집합 열 바인딩 해제 수 하기 전에 응용 프로그램 호출 해야 **SQLCloseCursor** 또는 **SQLFreeStmt** SQL_CLOSE 옵션을 사용 합니다.
