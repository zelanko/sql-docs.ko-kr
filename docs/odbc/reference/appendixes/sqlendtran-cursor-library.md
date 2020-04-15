---
title: SQLEndTran (커서 라이브러리) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2277a67cd5410ea3c2a5d5b03b16d4533ed6ee1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304774"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLEndTran** 함수의 사용에 대해 설명합니다. **SQLEndTran에**대한 일반 정보는 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조하십시오.  
  
 커서 라이브러리는 트랜잭션을 지원하지 않으며 **SQLEndTran에** 대한 호출을 드라이버에 직접 전달합니다. 그러나 커서 라이브러리는 SQL_CURSOR_ROLLBACK_BEHAVIOR 및 SQL_CURSOR_COMMIT_BEHAVIOR 정보 형식을 사용하여 데이터 원본에서 반환되는 커서 커밋 및 롤백 동작을 지원합니다.  
  
-   트랜잭션 간에 커서를 보존하는 데이터 원본의 경우 데이터 원본에서 롤백된 변경 내용은 커서 라이브러리의 캐시에서 롤백되지 않습니다. 캐시가 데이터 원본의 데이터와 일치하도록 하려면 응용 프로그램이 커서를 닫고 다시 열어야 합니다.  
  
-   트랜잭션 경계에서 커서를 닫는 데이터 원본의 경우 커서 라이브러리는 커서를 닫고 연결의 모든 문에 대한 캐시를 삭제합니다.  
  
-   트랜잭션 경계에서 준비된 문을 삭제하는 데이터 원본의 경우 응용 프로그램은 다시 실행하기 전에 연결에 준비된 모든 문을 다시 준비해야 합니다.
