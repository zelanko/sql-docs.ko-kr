---
title: 오류 메시지 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bbf73940b92ef158e4e93b10c2142c9053703f5f
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705410"
---
# <a name="error-messages"></a>오류 메시지
  Native Client ODBC 드라이버에서 반환 하는 메시지의 텍스트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQLGetDiagRec**의 *MessageText* 매개 변수에 배치 됩니다. 오류의 원본은 메시지 헤더에 표시됩니다.  
  
 [Microsoft][ODBC Driver Manager]  
 이러한 오류는 ODBC 드라이버 관리자에서 발생됩니다.  
  
 [Microsoft][ODBC Cursor Library]  
 이러한 오류는 ODBC 커서 라이브러리에서 발생됩니다.  
  
 [Microsoft][SQL Server Native Client]  
 이러한 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버에 의해 발생 합니다. 이름이 Net-Library 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인 다른 노드가 없으면 드라이버에서 오류가 발생한 것입니다.  
  
 Microsoft [SQL Server Native Client] [*네트워크-이름*]  
 이러한 오류는 Net-library에 의해 발생 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 여기서 *net-udname* 은 클라이언트 네트워크 전송의 표시 이름 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (예: 명명 된 파이프, 공유 메모리, tcp/ip 소켓 또는 VIA)입니다. 나머지 오류 메시지에는 호출된 Net-Library 함수 및 TDS 함수에 의해 기본 네트워크 API에서 호출된 함수가 포함됩니다. 이러한 오류와 함께 반환 되는 *pfNative* 오류 코드는 기본 네트워크 프로토콜 스택의 오류 코드입니다.  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 이러한 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 발생됩니다. 나머지 오류 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 오류 메시지 텍스트입니다. 이러한 오류와 함께 반환 되는 *pfNative* 코드는의 오류 번호입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 에서 반환 될 수 있는 오류 메시지 목록 및 오류 메시지에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 **master** 데이터베이스에서 **sysmessages** 시스템 테이블의 설명 및 오류 열을 참조 하세요 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 메시지 처리](handling-errors-and-messages.md)  
  
  
