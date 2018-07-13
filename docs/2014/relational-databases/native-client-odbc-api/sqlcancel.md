---
title: SQLCancel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed3bdb4cc5c2508435bff011545b5b9113d7aeac
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424392"
---
# <a name="sqlcancel"></a>SQLCancel
  [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516) 항목에 따르면 odbc에서 2.x의 경우 응용 프로그램을 호출 하는 경우 `SQLCancel` 없습니다 처리 문에서 수행 되는 경우 `SQLCancel` 것과 동일한 효과가 `SQLFreeStmt` 사용 하 여를 `SQL_CLOSE` 옵션;이 참조용 으로만 동작이 정의 되 고 응용 프로그램을 호출 해야 `SQLFreeStmt` 또는 `SQLCloseCursor` 를 커서를 닫습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 응용 프로그램에서 ODBC API 버전을 3.5.x 이상으로 설정하는 경우에도 `SQLCancel` 함수는 ODBC 2.x 동작을 사용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
