---
title: SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47b0d30ac70ff3b7974f7d0530b9fb50494ac424
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354329"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
  [ODBC 프로그래머 참조(ODBC Programmer's Reference)](https://go.microsoft.com/fwlink/?LinkId=45250) 에는 ODBC 2. **x** 또는 ODBC 3.*x* API를 사용하도록 작성된 애플리케이션에서 ODBC 드라이버가*SQLSetEnvAttr* 특성 사양을 해석하는 방법이 정의되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 이러한 규칙을 준수합니다.  
  
 **SQLSetEnvAttr** 은 연결 풀링을 사용할지 여부를 제어하는 특성 중 하나를 갖습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 연결 풀링을 사용하려면 *SQLDriverConnect* 또는 [SQLConnect](sqldriverconnect.md) 를 사용하여 연결할 때 **DriverCompletion**매개 변수를 SQL_DRIVER_NOPROMPT로 설정해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLSetEnvAttr 함수](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
