---
title: SQLTransact (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299223"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 코어 레벨  
  
 연결과 연관된 모든 명령문*핸들(hstmt*s)의 모든 활성 작업에 대한 커밋 또는 롤백 작업을 요청하거나 환경 핸들, *henv와*관련된 모든 연결에 대해 요청합니다. **SQLTransact는** 데이터베이스인 데이터 원본에만 [작동합니다.](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
 수동 모드에서 커밋이 실패하면 트랜잭션은 활성 상태로 유지됩니다. 트랜잭션을 롤백하거나 커밋 작업을 다시 시도할 수 있습니다. 자동 트랜잭션 모드에서 커밋 작업이 실패하면 트랜잭션이 자동으로 롤백됩니다. 트랜잭션이 비활성 상태일 수 없습니다.  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLTransact를](../../odbc/reference/syntax/sqltransact-function.md) 참조하십시오.
