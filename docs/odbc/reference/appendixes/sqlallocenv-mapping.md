---
title: "SQLAllocEnv 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1061472d46a49ca105fb970b19a2f2d950470a12
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv 매핑
응용 프로그램 호출 하는 경우 **SQLAllocEnv** ODBC 3*.x* 드라이버에 대 한 호출 **SQLAllocEnv**(*phenv*) 에매핑된**SQLAllocHandle** 다음과 같습니다.  
  
1.  드라이버 관리자 환경 핸들을 할당 하는 응용 프로그램에 반환 합니다. 드라이버 관리자를 호출 하 여 **SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION 환경 특성 SQL_OV_ODBC2을로 설정 합니다.  
  
2.  드라이버에 첫 번째 연결을 설정 하는 응용 프로그램, 드라이버 관리자 호출  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     사용 하 여 드라이버에서 *OutputHandlePtr* 로 설정 *phenv*합니다.
