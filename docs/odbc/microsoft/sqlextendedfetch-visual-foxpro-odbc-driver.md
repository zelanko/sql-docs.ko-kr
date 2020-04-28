---
title: SQLExtendedFetch (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ecff538198a2b517f980cc63acfc97d29a9f162
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298653"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 2  
  
 [Sqlfetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) 와 유사 하지만 각 열에 대해 배열을 사용 하 여 여러 행을 반환 합니다. 결과 집합은 앞으로 스크롤할 수 있으며 커서가 전진 전용이 아닌 정적으로 정의 된 경우에는 뒤로 스크롤할 수 있습니다.  
  
 기본적으로 Visual FoxPro ODBC 드라이버는 FoxPro 테이블에서 삭제 된 것으로 표시 된 행을 반환 하지 않습니다. 삭제 하도록 표시 되었지만 테이블에서 아직 제거 되지 않은 행은 결과 집합 커서에 포함 되지 않습니다. [SET DELETED](../../odbc/microsoft/set-deleted-command.md) 명령을 사용 하 여이 동작을 변경할 수 있습니다.  
  
 자세한 내용은 *ODBC 프로그래머 참조*에서 [sqlextendedfetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) 를 참조 하세요.
