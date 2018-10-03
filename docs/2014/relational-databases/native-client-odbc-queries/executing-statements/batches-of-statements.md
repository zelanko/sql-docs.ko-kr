---
title: 문의 일괄 처리 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC], batches
- batches [ODBC]
- ODBC applications, statements
- multiple statements, batches
- SQLMoreResults function
- SQLExecDirect function
ms.assetid: 057d7c1c-1428-4780-9447-a002ea741188
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aa97baae4ad6331193cab16ae2609212753c5be0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051941"
---
# <a name="batches-of-statements"></a>문의 일괄 처리
  일괄 처리 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문은 세미콜론 (;)에 전달 된 단일 문자열에 두 개 이상의 문을 포함 **SQLExecDirect** 하거나 [SQLPrepare 함수](http://go.microsoft.com/fwlink/?LinkId=59360)합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 일괄 처리를 사용하면 대개 네트워크 트래픽이 줄어들므로 문을 개별적으로 전송하는 것보다 효율적일 수 있습니다. 사용 하 여 [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) 를 다음 결과 집합의 현재 결과 집합을 사용 하 여 완료 되 면에서 위치를 지정 합니다.  
  
 ODBC 커서 특성을 행 집합 크기가 1인 정방향 전용의 읽기 전용 커서(기본값)로 설정하면 항상 일괄 처리를 사용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대해 서버 커서를 사용할 때 일괄 처리를 실행하면 서버 커서가 암시적으로 기본 결과 집합으로 변환됩니다. **SQLExecDirect** 또는 **SQLExecute** SQL_SUCCESS_WITH_INFO를 호출과 반환 **SQLGetDiagRec** 반환 합니다.  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>관련 항목  
 [문 실행 &#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
