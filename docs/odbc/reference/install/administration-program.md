---
title: 관리 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f7b3f0420fa7f0ed2226201d06a339341f5f734
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="administration-program"></a>관리 프로그램
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC만 명시적으로 설치 해야 합니다.  
  
 관리 프로그램을 ODBC 관리자는 Windows SDK/MDAC sdk에 포함 되어 있습니다. 이 프로그램 및 SDK의 사용자가 재배포할 수 있습니다. 또한 개발자는 자신의 관리 프로그램을 작성할 수 있습니다. 일반적으로 개발자 완벽 하 게 데이터 소스 구성 제어를 유지 하려고 하거나 관리 프로그램으로 사용 되는 응용 프로그램에서 직접 데이터 소스를 구성 하는 것만 자신의 관리 프로그램을 작성 합니다. 예를 들어 스프레드시트 프로그램을 추가한 다음 데이터 소스를 사용 하 여 런타임 시 사용자가 통합할 수 있습니다.  
  
 먼저 관리 프로그램 설치 프로그램 DLL을 로드합니다. 다음 작업을 수행 하려면 DLL이 설치 관리자에서 다음 함수를 호출 합니다.  
  
-   **추가, 수정 또는 대화형으로 데이터 원본을 삭제 합니다.** 관리 프로그램에서 호출할 수 **SQLManageDataSources**, **SQLCreateDataSource**, 또는 **SQLConfigDataSource**합니다.  
  
     **SQLManageDataSources** 와 사용자 추가, 수정 또는 데이터 원본을 삭제 하 고 수 추적 옵션을 지정; DLL 설치 관리자는 제어판에서 직접 호출 되 면이 함수가 호출 될 대화 상자가 표시 됩니다. **SQLCreateDataSource** 있는 사용자만 추가할 수 데이터 원본 대화 상자를 표시 합니다. **SQLConfigDataSource** 직접 드라이버 설치 DLL에 대 한 호출을 전달 합니다.  
  
     모든 경우에는 설치 관리자 DLL 호출 **ConfigDSN** 드라이버 설치 DLL 실제로 추가할 수정 또는 데이터 원본을 삭제 합니다. 드라이버 설치 DLL에는 추가 정보에 대 한 사용자를 표시 될 수 있습니다.  
  
-   **추가, 수정 또는 데이터 원본을 자동으로 삭제 합니다.** 관리 프로그램 호출 **SQLConfigDataSource** 설치 DLL 및 전달에는 null 창 처리할 것, 추가, 수정 또는 삭제 하는 데이터 원본의 이름과 레지스트리에 대 한 값의 목록입니다. 설치 프로그램 DLL 호출 하 여 **ConfigDSN** 드라이버 설치 DLL 실제로 추가할 수정 또는 데이터 원본을 삭제 합니다.  
  
-   **추가, 수정 또는 기본 데이터 원본을 삭제 합니다.** 기본 데이터 원본은 해당 이름이 기본 제외 하 고 다른 데이터 원본으로 같습니다. 추가, 수정 하거나 동일한 방식으로 다른 데이터 소스에서 삭제 합니다.
