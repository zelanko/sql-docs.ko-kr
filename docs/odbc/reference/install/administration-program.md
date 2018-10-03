---
title: 관리 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 740a09d9a6bceb9d3f290faa71444df0d1e7c6c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792321"
---
# <a name="administration-program"></a>관리 프로그램
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC를 명시적으로 설치 해야 합니다.  
  
 ODBC 관리자 관리 프로그램을 Windows SDK/MDAC SDK가 포함 되어 있습니다. 이 프로그램 및 SDK의 사용자가 재배포할 수 있습니다. 또한 개발자는 자신의 관리 프로그램을 작성할 수 있습니다. 일반적으로 개발자는 관리 프로그램 역할을 하는 응용 프로그램에서 직접 데이터 원본을 구성 하는 경우 또는 데이터 원본 구성 완전히 제어를 유지 하려고 하는 경우에 자신의 관리 프로그램을 작성 합니다. 예를 들어 스프레드시트 프로그램을 추가한 다음 데이터 소스를 사용 하 여 런타임 시 사용자를 수 있습니다.  
  
 먼저 관리 프로그램 설치 관리자 DLL을 로드합니다. 그런 다음 설치 관리자는 다음 작업을 수행 하는 DLL에서 함수를 호출 합니다.  
  
-   **추가, 수정 또는 대화형으로 데이터 원본을 삭제 합니다.** 관리 프로그램 호출할 수 있습니다 **SQLManageDataSources**하십시오 **SQLCreateDataSource**, 또는 **SQLConfigDataSource**합니다.  
  
     **SQLManageDataSources** 있는 사용자 추가, 수정 또는 데이터 원본을 삭제 하 고 수 추적 옵션을 지정; DLL 설치 관리자는 제어판에서 직접 호출 되 면이 함수가 호출 될 대화 상자를 표시 합니다. **SQLCreateDataSource** 있는 사용자만 추가할 수 데이터 원본 대화 상자를 표시 합니다. **SQLConfigDataSource** 드라이버 설치 DLL 직접 호출을 전달 합니다.  
  
     모든 경우에는 설치 관리자 DLL 호출 **ConfigDSN** 드라이버 설치 DLL이 실제로 추가, 수정 또는 데이터 원본을 삭제 합니다. 드라이버 설치 DLL에는 추가 정보에 대 한 사용자 라는 메시지가 표시 될 수 있습니다.  
  
-   **추가, 수정 또는 데이터 소스를 자동으로 삭제 합니다.** 관리 프로그램 호출 **SQLConfigDataSource** 설치 관리자 DLL에 전달 null 창을 처리할 것을 추가, 수정 또는 삭제는 데이터 원본의 이름 및 레지스트리에 대 한 값의 목록입니다. 설치 관리자 DLL 호출 **ConfigDSN** 드라이버 설치 DLL이 실제로 추가, 수정 또는 데이터 원본을 삭제 합니다.  
  
-   **추가, 수정 또는 기본 데이터 원본을 삭제 합니다.** 기본 데이터 원본의 이름과 기본은 점을 제외 하 고 다른 데이터 소스와 같습니다. 추가, 수정 또는 다른 데이터 원본으로 동일한 방식으로 삭제 됩니다.
