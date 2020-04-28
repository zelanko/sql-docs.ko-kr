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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c73ea704b091bc37afb1ac42b520304022d929c3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296273"
---
# <a name="registry-entries-for-data-sources"></a>데이터 원본에 대한 레지스트리 항목
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC는 Windows 운영 체제에 포함 되어 있습니다. ODBC는 이전 버전의 Windows에만 명시적으로 설치 해야 합니다.  
  
 설치 관리자 DLL은 각 데이터 원본에 대 한 정보를 레지스트리에 유지 관리 합니다. Microsoft Windows NT/Windows 2000 및 Microsoft Windows 95/98에서이 정보는 레지스트리의 다음 두 키 중 하나에 있는 하위 키에 저장 됩니다.  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbc.ini  
 ```

 ```console
 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini
 ```

 사용 되는 키는 데이터 원본이 *시스템 데이터 원본* (모든 사용자가 사용할 수 있음) 인지 아니면 현재 사용자만 사용할 수 있는 *사용자 데이터* 원본 인지에 따라 달라 집니다. 시스템 데이터 원본은 HKEY_LOCAL_MACHINE 트리에 저장 되 고 사용자 데이터 원본은 HKEY_CURRENT_USER 트리에 저장 됩니다. 다른 모든 측면에서 시스템 데이터 원본 및 사용자 데이터 원본은 동일 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC 데이터 원본 하위 키](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [데이터 소스 사양 하위 키](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [기본 하위 키](../../../odbc/reference/install/default-subkey.md)  
  
-   [ODBC 하위 키](../../../odbc/reference/install/odbc-subkey.md)
