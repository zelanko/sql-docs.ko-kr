---
title: SQLAllocEnv 매핑 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afbd1404cb40408166ecfc59993db7b183ae5ed2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68065013"
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv 매핑
응용 *프로그램이 ODBC 3.x* 드라이버를 통해 **sqlallocenv** 를 호출 하면 **sqlallocenv**(*phenv*)에 대 한 호출이 다음과 같이 **SQLAllocHandle** 에 매핑됩니다.  
  
1.  드라이버 관리자는 환경 핸들을 할당 하 고 응용 프로그램에 반환 합니다. 드라이버 관리자는 **SQLSetEnvAttr** 를 호출 하 여 SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC2로 설정 합니다.  
  
2.  응용 프로그램에서 드라이버에 대 한 첫 번째 연결을 설정 하면 드라이버 관리자에서 다음을 호출 합니다.  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     *OutputHandlePtr* 가 *phenv*로 설정 된 드라이버에서.
