---
title: 문 실행 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: rothja
ms.author: jroth
ms.openlocfilehash: 01dc4298855fd3418029164dea3ed089185da934
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018420"
---
# <a name="executing-statements-odbc"></a>문 실행(ODBC)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 데이터베이스에서 SQL 문을 실행 하는 다양 한 방법을 제공 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   직접 실행  
  
-   준비된 실행  
  
 직접 실행에는 문을 포함 하는 문자열을 작성 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 하 고 **Sqlexecdirect** 함수를 사용 하 여 실행을 위해 제출 해야 합니다. 준비된 실행에서는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문이 포함된 문자열을 작성한 다음 두 가지 단계로 실행합니다. 첫 번째 단계에서는 [Sqlprepare 함수](https://go.microsoft.com/fwlink/?LinkId=59360) 함수를 사용 하 여의 문에 대 한 실행 계획을 구문 분석 하 고 컴파일합니다 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] . 두 번째 단계는 **Sqlexecute** 함수를 사용 하 여 이전에 준비 된 실행 계획을 실행 합니다. 이렇게 하면 각각의 실행에서 구문 분석 및 컴파일 오버헤드를 줄일 수 있습니다. 준비된 실행은 애플리케이션에서 매개 변수가 있는 동일한 SQL 문을 반복적으로 실행하는 데 많이 사용됩니다.  
  
 직접 실행과 준비된 실행에서 모두 단일 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문이나 SQL 문의 일괄 처리를 실행하거나 저장 프로시저를 호출할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [직접 실행](direct-execution.md)  
  
-   [준비된 실행](prepared-execution.md)  
  
-   [절차](procedures.md)  
  
-   [문의 일괄 처리](batches-of-statements.md)  
  
-   [ISO 옵션의 효과](effects-of-iso-options.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;쿼리 실행](../executing-queries-odbc.md)  
  
  
