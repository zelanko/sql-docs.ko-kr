---
title: "대체 방법: SQL 문을 사용 하 여 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c1d1da58832a1fbbc133c17f58d940d46f5c6e1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="alternatives-using-sql-statements"></a>대체 방법: SQL 문 사용
ADO는 명령을 기본 제공 속성 및 데이터를 편집 하기 위한 메서드를 사용 하 여 수도 있습니다. 공급자에 따라,이 섹션에 언급 된 모든 작업도 가능 데이터 원본에 명령을 전달 합니다. SQL UPDATE 문을 사용 하지 않고 데이터를 수정 하려면 예를 들어 사용할 수는 **값** 속성은 **필드**합니다. ADO 메서드가 아니라 데이터 원본에 새 레코드를 추가 SQL insert를 사용할 수 **AddNew**합니다. SQL 또는 공급자의 데이터 조작 언어에 대 한 자세한 내용은 데이터 원본의 설명서를 참조 합니다.  
  
 예를 들어 다음 코드에 나와 있는 것 처럼 데이터베이스에 DELETE 문을 포함 하는 SQL 문자열을 전달할 수 있습니다.  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```

