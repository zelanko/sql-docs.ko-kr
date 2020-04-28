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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3910f24578bcbc409a84573e994c0680ed5949b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299223"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 코어 수준  
  
 연결과 관련 된 모든 문 핸들 (*hstmt*s)에 대 한 모든 활성 작업에 대해 커밋 또는 롤백 작업을 요청 하거나, 환경 핸들과 연결 된 모든 연결에 대해 *henv*를 요청 합니다. **Sqltransact** 은 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)의 데이터 원본에 대해서만 작동 합니다.  
  
 수동 모드에서 커밋이 실패할 경우 트랜잭션은 활성 상태로 유지 됩니다. 트랜잭션을 롤백하거나 커밋 작업을 다시 시도 하도록 선택할 수 있습니다. 자동 트랜잭션 모드에서 커밋 작업이 실패 하는 경우 트랜잭션은 자동으로 롤백됩니다. 트랜잭션을 비활성화할 수 없습니다.  
  
 자세한 내용은 *ODBC 프로그래머 참조*에서 [sqltransact](../../odbc/reference/syntax/sqltransact-function.md) 을 참조 하세요.
