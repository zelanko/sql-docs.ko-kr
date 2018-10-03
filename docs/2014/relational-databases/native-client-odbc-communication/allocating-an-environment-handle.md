---
title: 환경 핸들 할당 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66afa14ccb1953265f526f8c8861237638f569fd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151273"
---
# <a name="allocating-an-environment-handle"></a>환경 핸들 할당
  응용 프로그램에서 ODBC 함수를 호출하려면 먼저 ODBC 환경을 초기화하고 환경 핸들을 할당해야 합니다. 이 핸들은 전역 컨텍스트 핸들이고 ODBC의 다른 핸들에 대한 자리 표시자입니다. 호출 하 여이 작업을 수행 **SQLAllocHandle** 사용 하 여 합니다 *HandleType* 매개 변수를 SQL_HANDLE_ENV로 설정 하 고 *InputHandle* SQL_NULL_HANDLE로 설정 합니다.  
  
 응용 프로그램은 환경 핸들을 할당한 후 환경 특성을 설정하여 사용할 ODBC 함수 호출 버전을 지정해야 합니다. ODBC 3을 사용 하도록 *x* 함수 호출 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) 사용 하 여 합니다 *특성* 매개 변수가 SQL_ATTR_ODBC_VERSION으로 설정 하 고 *ValuePtr* SQL_OV_로 설정 ODBC3 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server와의 통신 &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
