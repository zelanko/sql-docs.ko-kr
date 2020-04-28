---
title: SQLAllocConnect 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25e72cd3830cea8504983f4348f6c200261490f4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305524"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 매핑
응용 프로그램이 ODBC 3을 통해 **Sqlallocconnect** 를 호출 하는 경우 *x* 드라이버는 **sqlallocconnect**(*henv*, *phdbc*)에 대 한 호출이 다음과 같이 **SQLAllocHandle** 에 매핑됩니다.  
  
1.  드라이버 관리자는 연결을 할당 하 고 응용 프로그램에 반환 합니다.  
  
2.  응용 프로그램에서 연결을 설정 하면 드라이버 관리자가 다음을 호출 합니다.  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     *InputHandle* 가 *henv*로 설정 된 드라이버에서 *OutputHandlePtr* 를 *phdbc*로 설정 합니다.
