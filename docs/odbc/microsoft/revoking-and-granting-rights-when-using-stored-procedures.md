---
title: 저장 프로시저를 사용 하는 경우 권한 부여 및 취소 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e881201e4653a168faff2fa438be19c1ca37e9b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127959"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>저장 프로시저를 사용할 때 권한 취소 및 권한 부여
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Microsoft ODBC Driver for Oracle 사용자 권한을 부여 하 고 다음 저장된 프로시저에서 액세스 하는 테이블에 취소할 때 다음 오류 메시지를 반환 합니다.  
  
 SQL_ERROR=-1  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 잘못 된 매개 변수  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 구문 오류 또는 액세스 위반  
  
 Oracle OCI 함수 Odessp() 호출이이 시나리오에서 실패 하지만 기본 매개 변수를 구현 하기 위해 필요 합니다. 기본 테이블 사용 권한을 수정 된 후에 저장된 프로시저가 다시 실행 하기 전에 컴파일해야 합니다.
