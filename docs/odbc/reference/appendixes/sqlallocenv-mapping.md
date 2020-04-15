---
title: SQLAllocEnv 매핑 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb26e3443fabda2d6490c071b1f2668895e66b8d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304044"
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv 매핑
응용 프로그램이 ODBC *3.x* 드라이버를 통해 **SQLAllocEnv를** 호출하면 **SQLAllocEnv***(phenv)에*대한 호출은 다음과 같이 **SQLAllocHandle에** 매핑됩니다.  
  
1.  드라이버 관리자는 환경 핸들을 할당하고 응용 프로그램에 반환합니다. 드라이버 관리자는 **SQLSetEnvAttr을** 호출하여 SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC2 설정합니다.  
  
2.  응용 프로그램이 드라이버에 대한 첫 번째 연결을 설정하면 드라이버 관리자가 호출합니다.  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     *출력핸들Ptr이* 있는 드라이버에서 *phenv로*설정됩니다.
