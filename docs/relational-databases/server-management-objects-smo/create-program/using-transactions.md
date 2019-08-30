---
title: 트랜잭션 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eaa6406e04eddbba012cfb61d6ae82a73b7f30bb
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148678"
---
# <a name="using-transactions"></a>트랜잭션 사용
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Object)에서 트랜잭션 처리는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 통해 수행됩니다. 연결이 설정 되 면 개체의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> <xref:Microsoft.SqlServer.Management.Smo.Server> 속성에서 개체를참조합니다.<xref:Microsoft.SqlServer.Management.Common.ServerConnection> <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> 및 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A>과 같은 메서드는 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 개체 속성에 속합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SMO 프로그램 만들기](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
