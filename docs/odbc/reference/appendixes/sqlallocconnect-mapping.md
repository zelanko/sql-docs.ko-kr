---
title: "SQLAllocConnect 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0188c47d6abfd294dc1a9c20c04ea7d271443a18
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 매핑
응용 프로그램 호출 하는 경우 **SQLAllocConnect** ODBC 3. *x* 드라이버에 대 한 호출 **SQLAllocConnect**(*henv*, *phdbc*)에 매핑되어 **SQLAllocHandle** 다음과 같습니다.  
  
1.  드라이버 관리자는 한 연결을 할당 하 고 응용 프로그램에 반환 합니다.  
  
2.  드라이버 관리자를 호출 하는 응용 프로그램 연결을 설정 하는 경우  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     사용 하 여 드라이버에서 *InputHandle* 로 설정 *henv*, 및 *OutputHandlePtr* 로 설정 *phdbc*합니다.

