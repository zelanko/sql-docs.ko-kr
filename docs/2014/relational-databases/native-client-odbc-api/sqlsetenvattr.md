---
title: SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 663d274b13a8cc5ac8ac53a2d8f9da4f925c7d55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181574"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
  [ODBC 프로그래머 참조(ODBC Programmer's Reference)](http://go.microsoft.com/fwlink/?LinkId=45250) 에는 ODBC 2. **x** 또는 ODBC 3.*x* API를 사용하도록 작성된 응용 프로그램에서 ODBC 드라이버가*SQLSetEnvAttr* 특성 사양을 해석하는 방법이 정의되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 이러한 규칙을 준수합니다.  
  
 **SQLSetEnvAttr** 은 연결 풀링을 사용할지 여부를 제어하는 특성 중 하나를 갖습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 연결 풀링을 사용하려면 *SQLDriverConnect* 또는 [SQLConnect](sqldriverconnect.md) 를 사용하여 연결할 때 **DriverCompletion**매개 변수를 SQL_DRIVER_NOPROMPT로 설정해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLSetEnvAttr 함수](http://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  