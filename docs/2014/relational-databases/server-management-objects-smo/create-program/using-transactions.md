---
title: 트랜잭션 사용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 83baa905887609e89b372d4820346ab9aa97a056
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63192020"
---
# <a name="using-transactions"></a>트랜잭션 사용
  SMO([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Object)에서 트랜잭션 처리는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체를 사용하여 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 인스턴스에 대한 연결을 통해 수행됩니다. 연결이 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 설정 되 면 개체의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> <xref:Microsoft.SqlServer.Management.Smo.Server> 속성에서 개체를 참조 합니다. 
  <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> 및 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A>과 같은 메서드는 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 개체 속성에 속합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SMO 프로그램 만들기](creating-smo-programs.md)  
  
  
