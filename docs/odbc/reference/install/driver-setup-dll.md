---
title: 드라이버 설정 DLL | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0a2878591c92fe0b2070a295d9dc622c245c17e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306424"
---
# <a name="driver-setup-dll"></a>드라이버 설정 DLL
> [!NOTE]  
>  Windows XP 및 Windows 서버 2003을 시작으로 ODBC는 Windows 운영 체제에 포함되어 있습니다. 이전 버전의 Windows에서는 ODBC만 명시적으로 설치해야 합니다.  
  
 드라이버 설정 DLL에는 **ConfigDriver** 및 **ConfigDSN** 함수가 포함되어 있습니다. **ConfigDriver는** 레지스트리에 드라이버 관련 정보를 입력하는 등 드라이버별 설치 작업을 수행합니다. **ConfigDSN은** 레지스트리의 데이터 원본에 대한 드라이버 관련 정보를 유지 관리합니다. 이러한 함수에 대한 전체 설명은 [설치 DLL API 참조](../../../odbc/reference/syntax/setup-dll-api-reference.md)를 참조하십시오.  
  
 **ConfigDSN은** 레지스트리의 데이터 원본 정보를 유지 관리하기 위해 설치 관리자 DLL에서 다음 기능을 호출합니다.  
  
-   **SQLWriteDSNToIni**. 데이터 원본을 추가합니다.  
  
-   **SQLRemoveDSNIni**. 데이터 원본을 삭제합니다.  
  
-   **SQLWrite개인 프로필 문자열**. 데이터 원본 사양 하위 키아래에 드라이버별 값을 작성합니다.  
  
-   **SQLGet개인 프로필 문자열**. 데이터 원본 사양 하위 키에서 드라이버별 값을 읽습니다.  
  
-   **SQLGetTranslator**. 사용자에게 번역기 이름과 옵션을 묻는 메시지를 표시합니다. 이 함수는 번역기 설정 DLL에서 **ConfigTranslator를** 호출합니다.  
  
 드라이버 설정 DLL은 드라이버 개발자가 작성합니다. 드라이버 DLL 또는 별도의 DLL의 일부일 수 있습니다.
