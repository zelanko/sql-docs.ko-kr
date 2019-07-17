---
title: SQLEndTran (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f713f9a0c96aaf3798cf160e648404470e3a4363
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064505"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLEndTran** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLEndTran**를 참조 하십시오 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.  
  
 커서 라이브러리 트랜잭션을 지원 하지 않습니다 하 고에 대 한 호출을 전달 **SQLEndTran** 드라이버에 직접. 그러나 커서 라이브러리 SQL_CURSOR_ROLLBACK_BEHAVIOR 및 SQL_CURSOR_COMMIT_BEHAVIOR 정보 형식 사용 하 여 데이터 소스에서 반환 된 커서 commit 및 rollback 동작을 지원 하지 않습니다.  
  
-   트랜잭션 간 커서를 유지 하는 데이터 원본에 대 한 변경 내용은 데이터 원본에 롤백되는 롤백되지 않습니다 커서 라이브러리 캐시에서 합니다. 데이터 소스의 데이터와 일치 하는 캐시를 위해 응용 프로그램 닫은 후 다시 열어야 커서입니다.  
  
-   트랜잭션 경계에 커서를 닫을 데이터 원본에 대 한 커서 라이브러리 커서를 닫고 연결의 모든 문에 대해 캐시를 삭제 합니다.  
  
-   준비 된 문은 트랜잭션 경계를 삭제 하는 데이터 원본에 대 한 응용 프로그램을 종료할지 전에 연결에서 모든 준비 된 문은 reprepare 해야 합니다.
