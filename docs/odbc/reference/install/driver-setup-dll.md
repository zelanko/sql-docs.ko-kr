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
ms.openlocfilehash: df91638f91091940e00e7a6a19d0fd6cb700f85f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094159"
---
# <a name="driver-setup-dll"></a>드라이버 설정 DLL
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC는 Windows 운영 체제에 포함 되어 있습니다. ODBC는 이전 버전의 Windows에만 명시적으로 설치 해야 합니다.  
  
 드라이버 설치 DLL에는 **Configdriver** 및 **ConfigDSN** 함수가 포함 되어 있습니다. **Configdriver** 는 레지스트리에 드라이버 관련 정보를 입력 하는 등의 드라이버별 설치 작업을 수행 합니다. **ConfigDSN** 는 레지스트리의 데이터 원본에 대 한 드라이버 관련 정보를 유지 관리 합니다. 이러한 함수에 대 한 자세한 설명은 [SETUP DLL API Reference](../../../odbc/reference/syntax/setup-dll-api-reference.md)를 참조 하세요.  
  
 **ConfigDSN** 는 설치 관리자 DLL에서 다음 함수를 호출 하 여 레지스트리에서 데이터 원본 정보를 유지 관리 합니다.  
  
-   **Sqlwritedsntoini**. 데이터 원본을 추가합니다.  
  
-   **SQLRemoveDSNFromIni**. 데이터 원본을 삭제 합니다.  
  
-   **SQLWritePrivateProfileString**. 데이터 원본 사양 하위 키 아래에 드라이버별 값을 작성 합니다.  
  
-   **SQLGetPrivateProfileString**. 데이터 원본 사양 하위 키에서 드라이버 관련 값을 읽습니다.  
  
-   **SQLGetTranslator**. 사용자에 게 번역기 이름 및 옵션을 입력 하 라는 메시지를 표시 합니다. 이 함수는 translator 설정 DLL에서 **Configtranslator** 를 호출 합니다.  
  
 드라이버 설치 DLL은 드라이버 개발자가 작성 합니다. 드라이버 DLL 또는 별도의 DLL에 포함 될 수 있습니다.
