---
title: SQLGetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fc982405e1e5244b6d151c7475024590682cbc6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48114600"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  애플리케이션이 커서 이름을 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 커서를 생성할 때 애플리케이션의 커서 이름을 생성합니다. 애플리케이션은 **SQLGetCursorName** 을 사용하여 위치 지정 UPDATE 및 DELETE 문에 대해 드라이버에서 정의된 커서 이름을 검색할 수 있습니다. 애플리케이션에서 위치 지정 데이터 조작 문을 이용하기 위해 **SQLSetCursorName** 을 호출할 필요는 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLGetCursorName 함수](http://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
