---
title: filestream access level 서버 구성 옵션 | Microsoft Docs
description: "\"Filestream_access_level\" 옵션에 대해 자세히 알아봅니다. 이 옵션이 SQL Server 인스턴스에 대한 FILESTREAM 액세스 수준을 변경하는 방법을 확인합니다."
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 04205ee05e3c26cc807a3a6aa828152c20e4c3c7
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670956"
---
# <a name="filestream-access-level-server-configuration-option"></a>filestream access level 서버 구성 옵션
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  filestream_access_level 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이 인스턴스에 대한 FILESTREAM 액세스 수준을 변경할 수 있습니다.  
  
> [!NOTE]  
>  이 옵션이 적용되려면 먼저 FILESTREAM에 대한 Windows 관리 설정을 사용하도록 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 시 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 이러한 설정을 사용하도록 지정할 수 있습니다.  
  
|값|정의|  
|-----------|----------------|  
|0|이 인스턴스에 대한 FILESTREAM 지원을 해제합니다.|  
|1|[!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스에 FILESTREAM을 사용하도록 설정합니다.|  
|2|[!INCLUDE[tsql](../../includes/tsql-md.md)] 및 Win32 스트리밍 액세스에 FILESTREAM을 사용하도록 설정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 구성 - Filestream](../install-windows/install-sql-server.md)   
 [Enable and Configure FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
