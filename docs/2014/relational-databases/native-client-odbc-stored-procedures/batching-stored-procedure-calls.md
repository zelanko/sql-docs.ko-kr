---
title: 저장 프로시저 호출 일괄 처리 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], batching
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- batches [ODBC]
- ODBC CALL escape sequence
ms.assetid: b7f53e11-15f0-4602-8134-b166160888f0
author: rothja
ms.author: jroth
ms.openlocfilehash: a0df58ce59853ee15b863cbc7bce34041c37fee4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039509"
---
# <a name="batching-stored-procedure-calls"></a>저장 프로시저 호출 일괄 처리
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 적절 한 경우 서버에 대 한 저장 프로시저 호출을 자동으로 일괄 처리 합니다. 이 드라이버는 ODBC CALL 이스케이프 시퀀스가 사용된 경우에만 이러한 작업을 수행하고 [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE 문이 실행된 경우에는 수행하지 않습니다. 저장 프로시저 호출을 일괄 처리하면 서버 왕복 횟수가 줄어들고 성능이 대폭 향상됩니다.  
  
 여러 개의 ODBC CALL 이스케이프 시퀀스가 포함된 일괄 처리를 실행하면 드라이버가 서버에 대한 프로시저 호출을 일괄 처리합니다. 또한 드라이버는 ODBC CALL 이스케이프 시퀀스와 함께 바인딩된 매개 변수 배열이 사용된 경우에도 프로시저 호출을 일괄 처리합니다. 예를 들어 행 단위 또는 열 단위 매개 변수 바인딩을 사용 하 여 5 개의 요소가 포함 된 배열을 ODBC CALL SQL 문의 매개 변수에 바인딩하는 경우 **Sqlexecute** 또는 **sqlexecdirect** 를 호출 하면 드라이버에서 서버에 대 한 프로시저 호출이 5 개인 단일 일괄 처리를 보냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [저장 프로시저 실행](running-stored-procedures.md)  
  
  
