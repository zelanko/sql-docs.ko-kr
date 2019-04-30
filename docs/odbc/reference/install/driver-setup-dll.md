---
title: 드라이버 설치 DLL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 088c9b60861266bf99649343aec2e763097bf155
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198196"
---
# <a name="driver-setup-dll"></a>드라이버 설정 DLL
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC를 명시적으로 설치 해야 합니다.  
  
 드라이버 설치 DLL에는 **ConfigDriver** 하 고 **ConfigDSN** 함수입니다. **ConfigDriver** 레지스트리에 드라이버 관련 정보를 입력 하는 등의 드라이버 관련 설치 작업을 수행 합니다. **ConfigDSN** 레지스트리에서 데이터 원본에 대 한 드라이버 관련 정보를 유지 관리 합니다. 에 대 한 전체 설명은 이러한 함수를 참조 하세요 [설치 DLL API 참조](../../../odbc/reference/syntax/setup-dll-api-reference.md)합니다.  
  
 **ConfigDSN** DLL 레지스트리에서 데이터 원본 정보를 유지 하기 위해 설치 관리자에서 다음 함수를 호출 합니다.  
  
-   **SQLWriteDSNToIni**. 데이터 소스를 추가 합니다.  
  
-   **SQLRemoveDSNFromIni**. 데이터 원본을 삭제 합니다.  
  
-   **SQLWritePrivateProfileString**. 데이터 소스 사양 하위 키 아래에 있는 드라이버 관련 값을 작성 합니다.  
  
-   **SQLGetPrivateProfileString**. 데이터 소스 사양 하위 키에서 드라이버 관련 값을 읽습니다.  
  
-   **SQLGetTranslator**. Translator 이름과 옵션에 대 한 사용자에 게 합니다. 이 함수 호출 **ConfigTranslator** 변환기에 DLL을 설치 합니다.  
  
 드라이버 설치 DLL 드라이버 개발자가 기록 됩니다. 드라이버의 일부일 수 있습니다 DLL 또는 별도 DLL입니다.
