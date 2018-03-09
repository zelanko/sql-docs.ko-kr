---
title: "SQLTransact (Visual FoxPro ODBC 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ff927598bd1c5458d296a4b19786c4c78b98785f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 핵심 수준  
  
 모든 문 핸들의 모든 활성 작업에 대 한 커밋 또는 롤백 작업을 요청 (*hstmt*s) 또는 환경 핸들에 연결 된 모든 연결에 대 한 연결와 관련 된 *henv*합니다. **SQLTransact** 인 데이터 원본에 대해서만 작동 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)합니다.  
  
 수동 모드에 있을 때 커밋 실패 하면 트랜잭션이 활성 상태로 유지 되; 트랜잭션을 롤백 또는 커밋 작업을 다시 시도를 선택할 수 있습니다. 자동 트랜잭션 모드에 있을 때 커밋 작업이 실패 하면 트랜잭션이 롤백됩니다 트랜잭션이 비활성화할 수 없습니다.  
  
 자세한 내용은 참조 [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) 에 *ODBC Programmer's Reference*합니다.
