---
title: SQLTransact (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e554a8669b6e6e95e234a5b939477a8bb2f7b8cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948861"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 코어 수준  
  
 모든 문 핸들의 모든 활성 작업에 대 한 커밋 또는 롤백 작업 요청 (*hstmt*s) 연결을 사용 하 여 환경 핸들을 사용 하 여 관련 된 모든 연결에 대 한 연결 된 *henv*합니다. **SQLTransact** 에 있는 데이터 원본에 대해서만 작동 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)합니다.  
  
 수동 모드에 있을 때 커밋 실패 하면 트랜잭션이 활성 상태로 유지 됩니다; 트랜잭션을 롤백 또는 커밋 작업을 다시 시도 하도록 선택할 수 있습니다. 자동 트랜잭션 모드에 있을 때 커밋 작업이 실패 하면, 트랜잭션이 자동으로 롤백됩니다. 트랜잭션이 비활성화할 수 없습니다.  
  
 자세한 내용은 [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) 에 *ODBC 프로그래머 참조*합니다.
