---
title: SQL Server Reporting Services Standard 및 Enterprise의 CPU 및 메모리 제한을 변경 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dd553715-2b95-4119-8f58-d01de388d9ab
caps.latest.revision: 11
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2f2511d378113539bfe8a1a9ccab43da99334f6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325453"
---
# <a name="changes-to-cpu-and-memory-limits-for-sql-server-reporting-services-standard-and-enterprise"></a>SQL Server Reporting Services Standard 및 Enterprise의 CPU 및 메모리 제한에 대한 변경입니다.
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services Standard 및 Enterprise에서는 최대 64GB의 시스템 메모리가 지원됩니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
### <a name="description"></a>Description  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services Standard 및 Enterprise에서는 최대 64GB의 시스템 메모리가 지원됩니다. 새로운 제한 사항에 맞게 현재 시스템 설정을 다시 구성해야 할 수 있습니다.  
  
 다른 버전의 CPU 및 메모리 제한에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [Compute Capacity Limits by Edition of SQL Server](../compute-capacity-limits-by-edition-of-sql-server.md), 및 [SQL Server 버전에서 지 원하는 메모리](http://go.microsoft.com/fwlink/?LinkId=212633)합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 새로운 CPU 및 메모리 제한 사항에 맞게 현재 시스템 설정을 다시 구성해야 할 수 있습니다. 자세한 내용은 [ALTER SERVER CONFIGURATION &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql), 및 [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014 버전에서 지 원하는 기능](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [이전 버전과의 호환성](../../../2014/getting-started/backward-compatibility.md)  
  
  
