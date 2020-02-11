---
title: 저장 프로시저를 사용할 때 권한 해지 및 권한 부여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91fcf722554fe1840465329e707c792a6bbab6db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987959"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>저장 프로시저를 사용할 때 권한 취소 및 권한 부여
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 용 Microsoft ODBC 드라이버는 사용자 권한을 부여 하 고 저장 프로시저에서 액세스 하는 테이블에 대해 취소 하면 다음 오류 메시지를 반환 합니다.  
  
 SQL_ERROR =-1  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 잘못 된 매개 변수 개수"  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 구문 오류 또는 액세스 위반  
  
 이 시나리오에서는 Oracle OCI 함수 Odessp ()에 대 한 호출이 실패 하지만 기본 매개 변수를 구현 하기 위해 필요 합니다. 기본 테이블 사용 권한이 수정 된 후 저장 프로시저를 다시 실행 하기 전에 다시 컴파일해야 합니다.
