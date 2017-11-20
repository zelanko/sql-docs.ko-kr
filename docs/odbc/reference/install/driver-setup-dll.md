---
title: "드라이버 설치 DLL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d75a8985feff2ddfe26d3e19e8bafd91f228d30e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="driver-setup-dll"></a>드라이버 설치 DLL
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC만 명시적으로 설치 해야 합니다.  
  
 드라이버 설치 DLL에 포함 되어는 **ConfigDriver** 및 **ConfigDSN** 함수입니다. **ConfigDriver** 레지스트리에 드라이버 관련 정보를 입력 하는 등의 드라이버 관련 설치 작업을 수행 합니다. **ConfigDSN** 레지스트리에서 데이터 원본에 대 한 드라이버 관련 정보를 유지 관리 합니다. 설명과 이러한 함수에 대 한 참조 [설치 DLL API 참조](../../../odbc/reference/syntax/setup-dll-api-reference.md)합니다.  
  
 **ConfigDSN** DLL 레지스트리에서 데이터 원본 정보를 유지 하기 위해 설치 프로그램에서 다음 함수를 호출 합니다.  
  
-   **SQLWriteDSNToIni**합니다. 데이터 원본을 추가 합니다.  
  
-   **SQLRemoveDSNFromIni**합니다. 데이터 원본을 삭제 합니다.  
  
-   **SQLWritePrivateProfileString**합니다. 데이터 원본 사양 하위 키 아래 드라이버 관련 값을 기록 합니다.  
  
-   **SQLGetPrivateProfileString**합니다. 데이터 원본 사양 하위 키에서 드라이버 관련 값을 읽기입니다.  
  
-   **SQLGetTranslator**합니다. 변환기 이름 및 옵션에 대 한 사용자 메시지를 표시 합니다. 이 함수 호출 **ConfigTranslator** 변환기에 DLL을 설치 합니다.  
  
 드라이버 설치 DLL 드라이버 개발자가 작성 됩니다. 드라이버의 일부가 될 수 있습니다 DLL 또는 별도 DLL입니다.

