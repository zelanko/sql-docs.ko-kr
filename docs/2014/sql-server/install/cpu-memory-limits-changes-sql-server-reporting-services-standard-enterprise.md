---
title: SQL Server Reporting Services Standard 및 Enterprise의 CPU 및 메모리 제한에 대 한 변경 내용 Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: dd553715-2b95-4119-8f58-d01de388d9ab
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4d8e18215c6078026b617e079879da1eadbca612
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66095958"
---
# <a name="changes-to-cpu-and-memory-limits-for-sql-server-reporting-services-standard-and-enterprise"></a>SQL Server Reporting Services Standard 및 Enterprise의 CPU 및 메모리 제한에 대한 변경입니다.
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services Standard 및 Enterprise에서는 최대 64GB의 시스템 메모리가 지원됩니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
### <a name="description"></a>Description  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services Standard 및 Enterprise에서는 최대 64GB의 시스템 메모리가 지원됩니다. 새로운 제한 사항에 맞게 현재 시스템 설정을 다시 구성해야 할 수 있습니다.  
  
 다른 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CPU 및 메모리 제한에 대 한 자세한 내용은 [SQL Server 버전별 계산 용량 제한](../compute-capacity-limits-by-edition-of-sql-server.md)및 [SQL Server 버전에서 지 원하는 메모리](https://go.microsoft.com/fwlink/?LinkId=212633)를 참조 하세요.  
  
## <a name="corrective-action"></a>수정 동작  
 새로운 CPU 및 메모리 제한 사항에 맞게 현재 시스템 설정을 다시 구성해야 할 수 있습니다. 자세한 내용은 [ALTER SERVER configuration &#40;transact-sql&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)및 [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014 버전에서 지 원하는 기능](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [이전 버전과의 호환성](../../../2014/getting-started/backward-compatibility.md)  
  
  
