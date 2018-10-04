---
title: 원시 오류 번호 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e7cd24a3eb1ccdeea1b6e6cbb97e2d0f222193f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180283"
---
# <a name="native-error-numbers"></a>원시 오류 번호
  데이터 원본에서 발생 하는 오류에 대 한 (반환한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 반환 된 원시 오류 번호를 반환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 드라이버에 의해 발견 된 오류에 대 한는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 원시 오류 번호 0 반환 합니다. 원시 오류 번호 목록에 대 한 자세한 내용은 오류 열을 참조 합니다 **sysmessages** 시스템 테이블에는 **마스터** 데이터베이스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다.  
  
 상태 오류 코드에 대 한 자세한 내용은 [SQLSTATE &#40;ODBC 오류 코드&#41;](sqlstate-odbc-error-codes.md)합니다. Net-Library에서 반환된 오류의 경우 원시 오류 번호는 기본 네트워크 소프트웨어에서 가져온 것입니다.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 메시지 처리](handling-errors-and-messages.md)  
  
  
