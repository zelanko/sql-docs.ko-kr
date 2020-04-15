---
title: 저장 프로시저 사용 시 해지 및 권한 부여 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 469e6f0fdc6794e3bd163844e43821798aa4a617
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303989"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>저장 프로시저를 사용할 때 권한 취소 및 권한 부여
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 오라클용 Microsoft ODBC 드라이버는 사용자 권한이 부여된 후 저장 프로시저에서 액세스하는 테이블에서 해지될 때 다음과 같은 오류 메시지를 반환합니다.  
  
 SQL_ERROR=-1  
  
 szErrorMsg="[마이크로소프트][오라클용 ODBC 드라이버]잘못된 수의 매개변수"  
  
 szErrorMsg="[마이크로소프트][오라클용 ODBC 드라이버]구문 오류 또는 액세스 위반"  
  
 Oracle OCI 함수 Odessp()에 대한 호출은 이 시나리오에서 실패하지만 기본 매개 변수를 구현하기 위해 필요합니다. 기본 테이블 사용 권한이 수정된 후 저장 프로시저를 다시 실행하기 전에 다시 컴파일해야 합니다.
