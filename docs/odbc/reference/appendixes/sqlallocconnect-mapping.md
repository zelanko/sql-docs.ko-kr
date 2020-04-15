---
title: SQLAllocConnect 매핑 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305524"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 매핑
응용 프로그램이 ODBC 3을 통해 **SQLAllocConnect를** 호출할 때 *x* 드라이버, **SQLAllocConnect***(헨브*, *phdbc)에*대한 호출은 다음과 같이 **SQLAllocHandle에** 매핑됩니다 .  
  
1.  드라이버 관리자는 연결을 할당하고 응용 프로그램에 반환합니다.  
  
2.  응용 프로그램이 연결을 설정하면 드라이버 관리자가 호출합니다.  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     *입력 핸들이* *henv로*설정하고 *OutputHandlePtr가* *phdbc로*설정된 드라이버에서 .
