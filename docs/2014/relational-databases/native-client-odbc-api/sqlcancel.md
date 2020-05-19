---
title: SQLCancel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 54ec9ddb143e97aa61a47ebbf0d2094281e59964
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706369"
---
# <a name="sqlcancel"></a>SQLCancel
  [Sqlcancel](https://go.microsoft.com/fwlink/?LinkId=203516) 토픽에서는 응용 프로그램이 `SQLCancel` 문에서 처리를 수행 하지 않을 때를 호출 하는 경우 옵션을 사용 하는 `SQLCancel` 것과 동일한 효과를 가집니다 `SQLFreeStmt` `SQL_CLOSE` .이 동작은 완전성을 위해서만 정의 되며 응용 프로그램은 `SQLFreeStmt` 또는를 호출 `SQLCloseCursor` 하 여 커서를 닫아야 합니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 애플리케이션에서 ODBC API 버전을 3.5.x 이상으로 설정하는 경우에도 `SQLCancel` 함수는 ODBC 2.x 동작을 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
