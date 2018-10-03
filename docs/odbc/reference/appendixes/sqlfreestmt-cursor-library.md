---
title: SQLFreeStmt (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 07d56e9b77c7e7e34b0de98ef5704b26aa2b86dd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854791"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLFreeStmt** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLFreeStmt**를 참조 하십시오 [SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)합니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLFreeStmt** 호출한 후 SQL_UNBIND 옵션과 **SQLExtendedFetch**하십시오 **SQLFetch**, 또는 **SQLFetchScroll**, 커서 라이브러리 오류를 반환 합니다. 응용 프로그램 결과 집합 열을 바인딩 해제할 수 고를 하기 전에 호출 해야 합니다 **SQLCloseCursor** 또는 **SQLFreeStmt** SQL_CLOSE 옵션을 사용 합니다.
