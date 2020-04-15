---
title: 관리 프로그램 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d8a2a8363371d6f6c3644c2b7b49aa77644d496e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306644"
---
# <a name="administration-program"></a>관리 프로그램
> [!NOTE]  
>  Windows XP 및 Windows 서버 2003을 시작으로 ODBC는 Windows 운영 체제에 포함되어 있습니다. 이전 버전의 Windows에서는 ODBC만 명시적으로 설치해야 합니다.  
  
 관리 프로그램인 ODBC 관리자는 Windows SDK/MDAC SDK에 포함되어 있습니다. 이 프로그램은 SDK의 사용자가 재배포 할 수 있습니다. 또한 개발자는 자체 관리 프로그램을 작성할 수 있습니다. 일반적으로 개발자는 데이터 원본 구성에 대한 완전한 제어를 유지하려는 경우 또는 관리 프로그램 역할을 하는 응용 프로그램에서 직접 데이터 원본을 구성하는 경우에만 자체 관리 프로그램을 작성합니다. 예를 들어 스프레드시트 프로그램을 사용하면 사용자가 런타임에 데이터 원본을 추가한 다음 사용할 수 있습니다.  
  
 관리 프로그램은 먼저 설치 관리자 DLL을 로드합니다. 그런 다음 설치 관리자 DLL의 함수를 호출하여 다음 작업을 수행합니다.  
  
-   **데이터 원본을 대화식으로 추가, 수정 또는 삭제합니다.** 관리 프로그램은 **SQLManageDataSource,** **SQLCreateDataSource**또는 **SQLConfigDataSource를 호출할**수 있습니다.  
  
     **SQLManageDataSource는** 사용자가 데이터 원본을 추가, 수정 또는 삭제하고 추적 옵션을 지정할 수 있는 대화 상자를 표시합니다. 이 함수는 설치 프로그램 DLL이 제어판에서 직접 호출될 때 호출됩니다. **SQLCreateDataSource는** 사용자가 데이터 원본만 추가할 수 있는 대화 상자를 표시합니다. **SQLConfigDataSource** 드라이버 설정 DLL에 직접 호출을 전달합니다.  
  
     모든 경우에 설치 관리자 DLL은 드라이버 설치 DLL에서 **ConfigDSN을** 호출하여 데이터 원본을 실제로 추가, 수정 또는 삭제합니다. 드라이버 설정 DLL은 사용자에게 추가 정보를 묻는 메시지를 표시할 수 있습니다.  
  
-   **데이터 원본을 자동으로 추가, 수정 또는 삭제합니다.** 관리 프로그램은 설치 관리자 DLL에서 **SQLConfigDataSource를** 호출하고 null 창 핸들, 추가, 수정 또는 삭제할 데이터 원본의 이름 및 레지스트리의 값 목록을 전달합니다. 설치 관리자 DLL은 드라이버 설정 DLL에서 **ConfigDSN을** 호출하여 데이터 원본을 실제로 추가, 수정 또는 삭제합니다.  
  
-   **기본 데이터 원본을 추가, 수정 또는 삭제합니다.** 기본 데이터 원본은 이름이 기본값이라는 점을 제외하면 다른 데이터 원본과 동일합니다. 다른 데이터 원본과 동일한 방식으로 추가, 수정 또는 삭제됩니다.
