---
title: "트랜잭션을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 93335b496f798658f2840a1a02757ed0949b9760
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="using-transactions"></a>트랜잭션 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), 트랜잭션 처리의 인스턴스에 대 한 연결을 통해 얻습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 사용 하 여는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체입니다. <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 참조 하는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성은 <xref:Microsoft.SqlServer.Management.Smo.Server> 연결 되 면 개체입니다. <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> 및 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A>과 같은 메서드는 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 개체 속성에 속합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SMO 프로그램 만들기](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
