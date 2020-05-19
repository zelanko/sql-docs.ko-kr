---
title: 원시 오류 번호 | Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b9612fbd7dd50ffeec812532e25a63eecca26571
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705360"
---
# <a name="native-error-numbers"></a>원시 오류 번호
  에서 반환 하는 데이터 원본에서 발생 하는 오류의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버는에 의해 반환 된 원시 오류 번호를 반환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 드라이버에서 검색 된 오류의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 원시 오류 번호 0을 반환 합니다. 네이티브 오류 번호 목록에 대 한 자세한 내용은의 **master** 데이터베이스에서 **sysmessages** 시스템 테이블의 error 열을 참조 하십시오 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 상태 오류 코드에 대 한 자세한 내용은 [SQLSTATE &#40;ODBC 오류 코드&#41;](sqlstate-odbc-error-codes.md)를 참조 하세요. Net-Library에서 반환된 오류의 경우 원시 오류 번호는 기본 네트워크 소프트웨어에서 가져온 것입니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 메시지 처리](handling-errors-and-messages.md)  
  
  
