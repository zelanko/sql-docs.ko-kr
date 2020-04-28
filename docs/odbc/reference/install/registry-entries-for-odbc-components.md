---
title: ODBC 구성 요소에 대 한 레지스트리 항목 Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- installing ODBC components [ODBC], registry entries
- registry entries for components [ODBC]
- subkeys [ODBC], for components
- registry entries for components [ODBC], about registry entries
ms.assetid: c90aa8a4-6ece-48de-901c-17d23739a9ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bead63f11b253342cd444e1d5bd0697ee00cfbc1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296183"
---
# <a name="registry-entries-for-odbc-components"></a>ODBC 구성 요소에 대한 레지스트리 항목
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC는 Windows 운영 체제에 포함 되어 있습니다. ODBC는 이전 버전의 Windows에만 명시적으로 설치 해야 합니다.  
  
 설치 관리자 DLL은 설치 된 각 ODBC 구성 요소에 대 한 정보를 레지스트리에 보관 합니다. Microsoft Windows NT 및 Microsoft Windows 95/98를 실행 하는 컴퓨터에서이 정보는 레지스트리의 다음 키 아래에 있는 하위 키에 저장 됩니다.  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbcinst.ini
 ```

 Odbcinst.ini는 HKEY_LOCAL_MACHINE 트리의 하위 키 이므로 컴퓨터의 모든 사용자가 ODBC 구성 요소에 대 한 정보를 사용할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC 핵심 하위 키](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [ODBC 드라이버 하위 키](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [드라이버 사양 하위 키](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [기본 드라이버 하위 키](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [ODBC 변환기 하위 키](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [변환기 사양 서브 키](../../../odbc/reference/install/translator-specification-subkeys.md)
