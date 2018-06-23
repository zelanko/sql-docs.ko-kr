---
title: 오류 메시지 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2ba9c50f600caf23a6948752ce34e816e493a41b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081571"
---
# <a name="error-messages"></a>오류 메시지
  반환 된 메시지의 텍스트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 배치 되는 *MessageText* 의 매개 변수 **SQLGetDiagRec**합니다. 오류의 원본은 메시지 헤더에 표시됩니다.  
  
 [Microsoft][ODBC Driver Manager]  
 이러한 오류는 ODBC 드라이버 관리자에서 발생됩니다.  
  
 [Microsoft][ODBC Cursor Library]  
 이러한 오류는 ODBC 커서 라이브러리에서 발생됩니다.  
  
 [Microsoft][SQL Server Native Client]  
 이러한 오류에 의해 발생 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버. 이름이 Net-Library 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인 다른 노드가 없으면 드라이버에서 오류가 발생한 것입니다.  
  
 [Microsoft] [SQL Server Native Client] [*Net-transportname*]  
 이러한 오류에 의해 발생는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워크 라이브러리 여기서 *Net-transportname* 의 표시 이름인는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 네트워크 전송 (예를 들어 명명 된 파이프, 공유 메모리, TCP/IP 소켓 또는 VIA)입니다. 나머지 오류 메시지에는 호출된 Net-Library 함수 및 TDS 함수에 의해 기본 네트워크 API에서 호출된 함수가 포함됩니다. *pfNative* 이러한 오류와 함께 반환 된 오류 코드에서 기본 네트워크 프로토콜 스택의 오류 코드입니다.  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 이러한 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 발생됩니다. 나머지 오류 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 오류 메시지 텍스트입니다. *pfNative* 이러한 오류와 함께 반환 된 코드의 오류 번호는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 반환 될 수 있는 오류 메시지 (및 해당 번호)의 목록에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 설명 및 오류 열 참조는 **sysmessages** 시스템 테이블에는 **마스터** 여기에 데이터베이스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 메시지 처리](handling-errors-and-messages.md)  
  
  