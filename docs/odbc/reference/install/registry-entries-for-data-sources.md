---
title: 데이터 원본에 대 한 레지스트리 항목 | Microsoft Docs
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
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c225109657906459d86ab5d19e441158c16ca57d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="registry-entries-for-data-sources"></a>데이터 원본에 대 한 레지스트리 항목
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC만 명시적으로 설치 해야 합니다.  
  
 설치 관리자 DLL 레지스트리에서 각 데이터 원본에 대 한 정보를 유지 관리합니다. Microsoft Windows NT/Windows 2000 및 Microsoft Windows 95/98에서는이 정보는 레지스트리의 다음 두 키 중 하나에 속하는 하위 키에 저장 됩니다.  
  
 HKEY_LOCAL_MACHINE  
  
 소프트웨어  
  
 ODBC  
  
 Odbc.ini  
  
 HKEY_CURRENT_USER  
  
 소프트웨어  
  
 ODBC  
  
 Odbc.ini  
  
 데이터 원본 인지에 따라는 키를 사용 하는 *시스템 데이터 원본* 모든 사용자에 게 제공 되 또는 *사용자 데이터 원본* 은 현재 사용자에만 사용할 수 있습니다. 시스템 데이터 원본은 HKEY_LOCAL_MACHINE 트리에 저장 된 및 사용자 데이터 원본은 HKEY_CURRENT_USER 트리에 저장 됩니다. 다른 모든 측면에서 시스템 데이터 원본 및 데이터 원본을 사용자는 동일 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC 데이터 원본 하위 키](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [데이터 소스 사양 하위 키](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [기본 하위 키](../../../odbc/reference/install/default-subkey.md)  
  
-   [ODBC 하위 키](../../../odbc/reference/install/odbc-subkey.md)
