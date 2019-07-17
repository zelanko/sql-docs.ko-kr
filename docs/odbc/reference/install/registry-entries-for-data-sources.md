---
title: 데이터 원본에 대 한 레지스트리 항목 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0b9d101395a3276f92f3ccf49e36effc65420f7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093885"
---
# <a name="registry-entries-for-data-sources"></a>데이터 원본에 대한 레지스트리 항목
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC를 명시적으로 설치 해야 합니다.  
  
 설치 관리자 DLL 레지스트리에서 각 데이터 원본에 대 한 정보를 유지 관리합니다. Microsoft Windows NT/Windows 2000 및 Microsoft Windows 95/98에서는이 정보는 레지스트리의 다음 두 키 중 하나에서 하위 키에 저장 됩니다.  
  
 HKEY_LOCAL_MACHINE  
  
 소프트웨어  
  
 ODBC  
  
 Odbc.ini  
  
 HKEY_CURRENT_USER  
  
 소프트웨어  
  
 ODBC  
  
 Odbc.ini  
  
 데이터 원본 인지에 따라 달라 집니다는 키를 사용 하는 *시스템 데이터 원본* 모든 사용자에 게 제공 되 또는 *사용자 데이터 원본* 현재 사용자에만 사용할 수 있는 합니다. HKEY_LOCAL_MACHINE 트리에서 저장 된 시스템 데이터 원본 및 HKEY_CURRENT_USER 트리에서 사용자 데이터 원본을 저장 됩니다. 다른 모든 측면에서 시스템 데이터 원본 및 사용자 데이터 원본은 동일합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC 데이터 원본 하위 키](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [데이터 소스 사양 하위 키](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [기본 하위 키](../../../odbc/reference/install/default-subkey.md)  
  
-   [ODBC 하위 키](../../../odbc/reference/install/odbc-subkey.md)
