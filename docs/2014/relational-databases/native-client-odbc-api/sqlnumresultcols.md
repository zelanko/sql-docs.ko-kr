---
title: SQLNumResultCols | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c1a4825dc8d73f815f6b399c6e3a51c064d3b9b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424322"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  실행된 된 문의 경우에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 결과 집합에서 열 수를 보고 서버를 방문 하지 않습니다. 이 경우 `SQLNumResultCols` 서버 왕복은 발생 하지 않습니다. 와 같은 [SQLDescribeCol](sqldescribecol.md) 하 고 [SQLColAttribute](sqlcolattribute.md)호출, `SQLNumResultCols` 준비 되었지만 실행된 되지 않은 문에 서버 왕복이 생성 합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 문 일괄 처리에서 여러 결과 행 집합이 반환되는 경우 결과 집합 열의 수가 하나에서 다른 수로 변경될 수 있습니다. `SQLNumResultCols` 각 집합에 대해 호출 되어야 합니다. 열 수가 변경되면 응용 프로그램이 행 결과를 인출하기 전에 데이터 값을 다시 바인딩해야 합니다. 집합 반환을 여러 결과 처리 하는 방법에 대 한 자세한 내용은 [SQLMoreResults](sqlmoreresults.md)합니다.  
  
 부터 데이터베이스 엔진의 개선 사항 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SQLNumResultCols 예상된 결과 대 한 보다 정확한 설명의 얻을를 허용 합니다. 이전 버전의 SQLNumResultCols 반환한 값에서 다를 수 있습니다 이러한 보다 정확한 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [메타 데이터 검색](../native-client/features/metadata-discovery.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLNumResultCols 함수](http://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
