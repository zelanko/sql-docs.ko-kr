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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064505"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **Sqlendtran** 함수를 사용 하는 방법을 설명 합니다. **Sqlendtran**에 대 한 일반 정보는 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.  
  
 커서 라이브러리는 트랜잭션을 지원 하지 않으며 **Sqlendtran** 에 대 한 호출을 드라이버에 직접 전달 합니다. 그러나 커서 라이브러리는 SQL_CURSOR_ROLLBACK_BEHAVIOR 및 SQL_CURSOR_COMMIT_BEHAVIOR 정보 유형을 사용 하 여 데이터 원본에서 반환 되는 커서 커밋 및 롤백 동작을 지원 합니다.  
  
-   트랜잭션 간에 커서를 유지 하는 데이터 원본의 경우 데이터 원본에서 롤백하는 변경 내용은 커서 라이브러리의 캐시에서 롤백되지 않습니다. 캐시가 데이터 원본의 데이터와 일치 하도록 하려면 응용 프로그램에서 커서를 닫았다가 다시 열어야 합니다.  
  
-   트랜잭션 경계에서 커서를 닫는 데이터 원본의 경우 커서 라이브러리는 커서를 닫고 연결의 모든 문에 대 한 캐시를 삭제 합니다.  
  
-   트랜잭션 경계에서 준비 된 문을 삭제 하는 데이터 원본의 경우 응용 프로그램은 다시 실행 하기 전에 연결에서 준비 된 모든 문을 다시 준비 해야 합니다.
