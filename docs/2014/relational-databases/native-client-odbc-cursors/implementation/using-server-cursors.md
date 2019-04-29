---
title: 서버 커서를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cef56db912d786b6908271d0747fe45690e90536
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011845"
---
# <a name="using-server-cursors"></a>서버 커서 사용
  ODBC 응용 프로그램에서 ODBC 커서 특성 중 하나를 기본값 이외의 값으로 설정 하는 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 동일한 유형의 API 서버 커서를 구현 하는 서버를 요청 합니다. API 서버 커서가 사용되면 클라이언트의 메모리가 확보되고 클라이언트와 서버 간의 네트워크 트래픽이 줄어들 수 있습니다.  
  
 API 서버 커서의 단점은 현재 모든 SQL 문을 지원하지 않는다는 것입니다. API 서버 커서는 다음을 실행하는 데 사용할 수 없습니다.  
  
-   여러 결과 집합을 반환하는 일괄 처리 또는 저장 프로시저  
  
-   COMPUTE, COMPUTE BY, FOR BROWSE 또는 INTO 절을 포함하는 SELECT 문  
  
-   원격 저장 프로시저를 참조하는 EXECUTE 문  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결된 경우 서버 커서를 사용하는 이러한 특징이 있는 문을 실행하면 커서가 기본 결과 집합으로 변환됩니다. 그러나 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결된 경우에는 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목  
 [커서 구현 방법](how-cursors-are-implemented.md)  
  
  
