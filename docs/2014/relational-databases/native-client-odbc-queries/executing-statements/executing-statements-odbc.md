---
title: 문 실행 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b50d6e9cc46e9abdf46e2b3b0a184654d9074b8f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410772"
---
# <a name="executing-statements-odbc"></a>문 실행(ODBC)
  합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 SQL 문을 실행 하는 다양 한 방법을 제공을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스:  
  
-   직접 실행  
  
-   준비된 실행  
  
 직접 실행에서는 포함 하는 문자 문자열을 작성을 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문과 사용 하 여 실행에 대 한 제출 합니다 **SQLExecDirect** 함수. 준비된 실행에서는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문이 포함된 문자열을 작성한 다음 두 가지 단계로 실행합니다. 첫 번째 단계에서 사용 하는 [SQLPrepare 함수](http://go.microsoft.com/fwlink/?LinkId=59360) 함수를 구문 분석에서 문의 실행 계획을 컴파일하는 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]합니다. 두 번째 단계에서 사용 하 여 **SQLExecute** 이전에 준비 된 실행 계획을 실행 하는 함수입니다. 이렇게 하면 각각의 실행에서 구문 분석 및 컴파일 오버헤드를 줄일 수 있습니다. 준비된 실행은 응용 프로그램에서 매개 변수가 있는 동일한 SQL 문을 반복적으로 실행하는 데 많이 사용됩니다.  
  
 직접 실행과 준비된 실행에서 모두 단일 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문이나 SQL 문의 일괄 처리를 실행하거나 저장 프로시저를 호출할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [직접 실행](direct-execution.md)  
  
-   [준비된 실행](prepared-execution.md)  
  
-   [절차](procedures.md)  
  
-   [문 일괄 처리](batches-of-statements.md)  
  
-   [ISO 옵션의 효과](effects-of-iso-options.md)  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 실행 &#40;ODBC&#41;](../executing-queries-odbc.md)  
  
  
