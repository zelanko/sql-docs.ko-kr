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
manager: craigg
ms.openlocfilehash: bdb63e9610d00c0736f640b6f4c4d743f3335c7d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606241"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 매핑
응용 프로그램을 호출할 때 **SQLAllocConnect** 는 ODBC 3. *x* 드라이버, 호출 **SQLAllocConnect**(*henv*를 *phdbc*)에 매핑된 **SQLAllocHandle** 다음과 같습니다:  
  
1.  드라이버 관리자는 연결을 할당 하 고 응용 프로그램에 반환 합니다.  
  
2.  드라이버 관리자를 호출 하는 응용 프로그램에 연결 하는 경우  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     사용 하 여에서 *InputHandle* 로 설정 *henv*, 및 *OutputHandlePtr* 로 *phdbc*합니다.
