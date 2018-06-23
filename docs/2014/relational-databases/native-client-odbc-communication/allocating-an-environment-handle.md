---
title: 환경 핸들 할당 | Microsoft Docs
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
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 89bf5353b37858c12212eed4567e0bae7f49d77f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088855"
---
# <a name="allocating-an-environment-handle"></a>환경 핸들 할당
  응용 프로그램에서 ODBC 함수를 호출하려면 먼저 ODBC 환경을 초기화하고 환경 핸들을 할당해야 합니다. 이 핸들은 전역 컨텍스트 핸들이고 ODBC의 다른 핸들에 대한 자리 표시자입니다. 호출 하 여이 작업을 수행 **SQLAllocHandle** 와 *HandleType* 매개 변수를 SQL_HANDLE_ENV로 설정 하 고 *InputHandle* SQL_NULL_HANDLE로 설정 합니다.  
  
 응용 프로그램은 환경 핸들을 할당한 후 환경 특성을 설정하여 사용할 ODBC 함수 호출 버전을 지정해야 합니다. ODBC 3 사용 하려면. *x* 함수 호출 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) 와 *특성* 매개 변수를 sql_attr_odbc_version으로 설정 하 고 *ValuePtr* SQL_OV_로 설정 ODBC3 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server와 통신 &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  