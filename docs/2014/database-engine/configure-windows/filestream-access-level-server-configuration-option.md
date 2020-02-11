---
title: filestream access level 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 90b4ec97a3ab31c93e92219b96724b75d7f86425
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62782258"
---
# <a name="filestream-access-level-server-configuration-option"></a>filestream access level 서버 구성 옵션
  filestream_access_level 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이 인스턴스에 대한 FILESTREAM 액세스 수준을 변경할 수 있습니다.  
  
> [!NOTE]  
>  이 옵션이 적용되려면 먼저 FILESTREAM에 대한 Windows 관리 설정을 사용하도록 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 시 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 이러한 설정을 사용하도록 지정할 수 있습니다.  
  
|값|정의|  
|-----------|----------------|  
|0|이 인스턴스에 대한 FILESTREAM 지원을 해제합니다.|  
|1|[!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스에 FILESTREAM을 사용하도록 설정합니다.|  
|2|[!INCLUDE[tsql](../../includes/tsql-md.md)] 및 Win32 스트리밍 액세스에 FILESTREAM을 사용하도록 설정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 구성 - Filestream](../../sql-server/install/database-engine-configuration-filestream.md)   
 [Enable and Configure FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
