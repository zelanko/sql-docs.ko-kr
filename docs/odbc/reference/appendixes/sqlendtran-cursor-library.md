---
title: SQLEndTran (커서 라이브러리) | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a908fbb43a6c568fd536c7ea2f47a523de287f3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLEndTran** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLEndTran**, 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.  
  
 커서 라이브러리 트랜잭션을 지원 하지 않으면 및 전달에 대 한 호출 **SQLEndTran** 드라이버에 직접 합니다. 그러나 커서 라이브러리는 SQL_CURSOR_ROLLBACK_BEHAVIOR 및 SQL_CURSOR_COMMIT_BEHAVIOR 정보 형식 사용 하 여 데이터 소스에서 반환 된 커서 commit 및 rollback 동작 지원:  
  
-   트랜잭션에 걸쳐 커서를 유지 하는 데이터 원본에 대 한 데이터 원본에서 롤백된 변경 내용이 롤백되지 않습니다 커서 라이브러리의 캐시에 있습니다. 데이터 원본의 데이터와 일치 하는 캐시를 응용 프로그램 해야 닫았다가 커서입니다.  
  
-   트랜잭션 경계에서 커서를 닫습니다는 데이터 원본에 대 한 커서 라이브러리는 커서가 닫힙니다 하 고 연결의 모든 문에 대해 캐시를 삭제 합니다.  
  
-   준비 된 문은 트랜잭션 경계를 삭제 하는 데이터 원본에 대 한 응용 프로그램을 종료할지 하기 전에 연결에서 모든 준비 된 문을 reprepare 해야 합니다.
