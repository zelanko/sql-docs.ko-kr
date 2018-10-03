---
title: 오류 메시지 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 05a1094dd30c750cb1f0c9b268159a8923f19b8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787026"
---
# <a name="error-messages"></a>오류 메시지
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  반환 된 메시지의 텍스트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 배치 됩니다 합니다 *MessageText* 의 매개 변수 **SQLGetDiagRec**합니다. 오류의 원본은 메시지 헤더에 표시됩니다.  
  
 [Microsoft][ODBC Driver Manager]  
 이러한 오류는 ODBC 드라이버 관리자에서 발생됩니다.  
  
 [Microsoft][ODBC Cursor Library]  
 이러한 오류는 ODBC 커서 라이브러리에서 발생됩니다.  
  
 [Microsoft][SQL Server Native Client]  
 발생 하는 이러한 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버. 이름이 Net-Library 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인 다른 노드가 없으면 드라이버에서 오류가 발생한 것입니다.  
  
 [Microsoft] [SQL Server Native Client] [*Net-transportname*]  
 발생 하는 이러한 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Net-library 위치 *Net-transportname* 표시 이름입니다를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 네트워크 전송 (예: 명명 된 파이프, 공유 메모리, TCP/IP 소켓 또는 VIA). 나머지 오류 메시지에는 호출된 Net-Library 함수 및 TDS 함수에 의해 기본 네트워크 API에서 호출된 함수가 포함됩니다. 합니다 *pfNative* 이러한 오류와 함께 반환 된 오류 코드는 기본 네트워크 프로토콜 스택의 오류 코드입니다.  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 이러한 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 발생됩니다. 나머지 오류 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 오류 메시지 텍스트입니다. 합니다 *pfNative* 이러한 오류와 함께 반환 된 코드의 오류 번호는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 반환 될 수 있는 오류 메시지 (및 해당 번호)의 목록에 대 한 자세한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 설명 및 오류 열을 표시 합니다 **sysmessages** 시스템 테이블에 있는 **마스터** 데이터베이스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 메시지 처리](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
