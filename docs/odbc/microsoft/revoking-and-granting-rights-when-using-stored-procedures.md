---
title: 저장 프로시저를 사용 하 여 권한 부여 및 취소 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ed3fa04ffbb67f0c6ddeba677a411c9c99c4768
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>저장된 프로시저를 사용 하는 경우 호출 및 권한 부여 권한
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 Microsoft ODBC Driver for Oracle 사용자 권한을 부여 하 고 다음 저장된 프로시저에서 액세스 하는 테이블에 취소할 때 다음 오류 메시지를 반환 합니다.  
  
 SQL_ERROR = 1  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 잘못 된 매개 변수 수가"  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 구문 오류 또는 액세스 위반"  
  
 Oracle OCI 함수 Odessp() 호출이이 시나리오에서 실패 하지만 기본 매개 변수를 구현 하는 데 필요 합니다. 기본 테이블 사용 권한은 수정한 후 저장된 프로시저 다시 실행 하기 전에 컴파일해야 합니다.
