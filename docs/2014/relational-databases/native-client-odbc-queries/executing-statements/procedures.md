---
title: 프로시저 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d030d4fb12ce9217bbdb88f501a0b0674c5a5828
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206755"
---
# <a name="procedures"></a>절차
  저장 프로시저란 하나 이상의 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 포함하는 미리 컴파일된 실행 개체입니다. 저장 프로시저는 입/출력 매개 변수를 가질 수 있으며 정수 반환 코드를 반환할 수도 있습니다. 응용 프로그램에서는 카탈로그 함수를 사용하여 사용 가능한 저장 프로시저를 열거할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 대상으로 하는 ODBC 응용 프로그램은 직접 실행 방식으로만 저장 프로시저를 호출해야 합니다. 이전 버전에 연결할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 구현 [SQLPrepare 함수](https://go.microsoft.com/fwlink/?LinkId=59360) 임시 저장된 프로시저를 만들어 이라고 하는 다음에 **SQLExecute** . 가 헤드가 **SQLPrepare** 호출 대상 저장 프로시저와 저장 프로시저를 실행 하는 직접만 임시 저장된 프로시저를 만듭니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인스턴스에 연결된 경우에도 호출을 준비하려면 추가 네트워크 왕복이 필요하고 저장 프로시저 실행 계획만 호출하는 실행 계획을 작성해야 합니다.  
  
 ODBC 응용 프로그램에서는 저장 프로시저를 실행할 때 ODBC CALL 구문을 사용해야 합니다. ODBC CALL 구문을 사용하면 드라이버는 원격 프로시저 호출 메커니즘을 사용하여 프로시저를 호출하도록 최적화됩니다. 이 방법은 서버에 [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE 문을 보내는 데 사용되는 메커니즘에 비해 훨씬 효과적입니다.  
  
 자세한 내용은 [저장 프로시저 실행](../../native-client-odbc-stored-procedures/running-stored-procedures.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [문 실행 &#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
