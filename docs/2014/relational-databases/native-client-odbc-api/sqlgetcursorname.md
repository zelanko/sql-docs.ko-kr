---
title: SQLGetCursorName | Microsoft Docs
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
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8840a494cbf5d4b0cdf8c304da0a0f063fcebed
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427832"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  응용 프로그램이 커서 이름을 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 커서를 생성할 때 응용 프로그램의 커서 이름을 생성합니다. 응용 프로그램은 **SQLGetCursorName** 을 사용하여 위치 지정 UPDATE 및 DELETE 문에 대해 드라이버에서 정의된 커서 이름을 검색할 수 있습니다. 응용 프로그램에서 위치 지정 데이터 조작 문을 이용하기 위해 **SQLSetCursorName** 을 호출할 필요는 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLGetCursorName 함수](http://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
