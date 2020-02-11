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
ms.openlocfilehash: 9cb78dae32bb17598ee0e86c26e621be1b6362c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068549"
---
# <a name="administration-program"></a>관리 프로그램
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC는 Windows 운영 체제에 포함 되어 있습니다. ODBC는 이전 버전의 Windows에만 명시적으로 설치 해야 합니다.  
  
 관리 프로그램인 ODBC 관리자는 Windows SDK/MDAC SDK에 포함 되어 있습니다. 이 프로그램은 SDK 사용자가 재배포할 수 있습니다. 또한 개발자는 자신의 관리 프로그램을 직접 작성할 수도 있습니다. 일반적으로 개발자는 데이터 원본 구성에 대 한 완전 한 제어를 유지 하려는 경우 나 관리 프로그램으로 작동 하는 응용 프로그램에서 직접 데이터 원본을 구성 하는 경우에만 자체 관리 프로그램을 작성 합니다. 예를 들어 스프레드시트 프로그램을 사용 하 여 사용자가 런타임에 데이터 원본을 추가 하 고 사용할 수 있습니다.  
  
 관리 프로그램은 먼저 설치 관리자 DLL을 로드 합니다. 그런 다음 설치 관리자 DLL의 함수를 호출 하 여 다음 작업을 수행 합니다.  
  
-   **데이터 원본을 대화형으로 추가, 수정 또는 삭제 합니다.** 관리 프로그램은 **SQLManageDataSources**, **sqlcreatedatasource**또는 **SQLConfigDataSource**를 호출할 수 있습니다.  
  
     **SQLManageDataSources** 사용자가 데이터 원본을 추가, 수정 또는 삭제할 수 있는 대화 상자를 표시 하 고 추적 옵션을 지정 합니다. 이 함수는 설치 관리자 DLL이 제어판에서 직접 호출 될 때 호출 됩니다. **Sqlcreatedatasource** 는 사용자가 데이터 원본만 추가할 수 있는 대화 상자를 표시 합니다. **SQLConfigDataSource** 는 호출을 드라이버 설치 DLL로 직접 전달 합니다.  
  
     모든 경우에 설치 관리자 DLL은 드라이버 설치 DLL에서 **ConfigDSN** 를 호출 하 여 실제로 데이터 원본을 추가, 수정 또는 삭제 합니다. 드라이버 설치 DLL에서 사용자에 게 추가 정보를 묻는 메시지를 표시할 수 있습니다.  
  
-   **데이터 원본을 자동으로 추가, 수정 또는 삭제 합니다.** 관리 프로그램은 설치 관리자 DLL에서 **SQLConfigDataSource** 를 호출 하 고이를 null 창 핸들, 추가, 수정 또는 삭제할 데이터 원본의 이름 및 레지스트리의 값 목록으로 전달 합니다. 설치 관리자 DLL은 드라이버 설치 DLL에서 **ConfigDSN** 를 호출 하 여 실제로 데이터 원본을 추가, 수정 또는 삭제 합니다.  
  
-   **기본 데이터 원본을 추가, 수정 또는 삭제 합니다.** 기본 데이터 원본은 다른 데이터 원본과 동일 하지만 이름이 기본값 이라는 점이 다릅니다. 다른 데이터 원본과 동일한 방식으로 추가, 수정 또는 삭제 됩니다.
