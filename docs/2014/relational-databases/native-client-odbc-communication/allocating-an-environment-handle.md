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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c655b5e9a406c3e1881c9dd199a92666377918f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021122"
---
# <a name="allocating-an-environment-handle"></a>환경 핸들 할당
  애플리케이션에서 ODBC 함수를 호출하려면 먼저 ODBC 환경을 초기화하고 환경 핸들을 할당해야 합니다. 이 핸들은 전역 컨텍스트 핸들이고 ODBC의 다른 핸들에 대한 자리 표시자입니다. 이 작업을 수행 하려면 *HandleType* 매개 변수를 SQL_HANDLE_ENV로 설정 하 고 *InputHandle* 를 SQL_NULL_HANDLE으로 설정 하 여 **SQLAllocHandle** 를 호출 합니다.  
  
 애플리케이션은 환경 핸들을 할당한 후 환경 특성을 설정하여 사용할 ODBC 함수 호출 버전을 지정해야 합니다. ODBC 3을 사용 합니다. *x* 함수를 사용 하 여 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) 를 호출 합니다. 여기서 *특성* 매개 변수는 SQL_ATTR_ODBC_VERSION *로 설정 되 고,* 는 SQL_OV_ODBC3로 설정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server &#40;ODBC&#41;와 통신](communicating-with-sql-server-odbc.md)  
  
  
