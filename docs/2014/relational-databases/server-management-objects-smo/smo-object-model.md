---
title: SMO 개체 모델 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], object model
- SQL Server Management Objects, object model
ms.assetid: bd6e59b6-ca46-42c0-adb2-c9d64cf6e00b
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bbaf5430252c296313723509b0195cdf5573ced5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081781"
---
# <a name="smo-object-model"></a>SMO 개체 모델
  SMO 개체 모델은 개체의 계층으로 구성됩니다. <xref:Microsoft.SqlServer.Management.Smo.Server> 개체가 최상위 개체이고 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체 아래에 모든 인스턴스 클래스 개체가 있습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 클래스는 별도의 개체 계층을 포함하는 최상위 클래스입니다. <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 개체가 나타내는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 및 네트워크 설정의 WMI 공급자를 통해 사용할 수 있습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server> 및 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 개체 외에도 태스크나 작업을 나타내는 <xref:Microsoft.SqlServer.Management.Smo.Transfer>, <xref:Microsoft.SqlServer.Management.Smo.Backup> 또는 <xref:Microsoft.SqlServer.Management.Smo.Restore>와 같은 여러 가지 유틸리티 클래스가 있습니다.  
  
 SMO 개체 모델은 여러 개의 네임스페이스로 구성됩니다. 자세한 내용은 [SMO 네임 스페이스](smo-object-model-namespaces.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [SMO 개체 모델 다이어그램](smo-object-model-diagram.md)   
 [SMO 네임 스페이스](smo-object-model-namespaces.md)   
 [구성 관리용 WMI 공급자 개념](../wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  