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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65c23f41ea9176c460c8fb32ece5e74dfb803541
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68065019"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 매핑
응용 프로그램이 ODBC 3을 통해 **Sqlallocconnect** 를 호출 하는 경우 *x* 드라이버는 **sqlallocconnect**(*henv*, *phdbc*)에 대 한 호출이 다음과 같이 **SQLAllocHandle** 에 매핑됩니다.  
  
1.  드라이버 관리자는 연결을 할당 하 고 응용 프로그램에 반환 합니다.  
  
2.  응용 프로그램에서 연결을 설정 하면 드라이버 관리자가 다음을 호출 합니다.  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     *InputHandle* 가 *henv*로 설정 된 드라이버에서 *OutputHandlePtr* 를 *phdbc*로 설정 합니다.
