---
title: ADOMD.NET에서 트랜잭션 수행 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- transactions [ADOMD.NET]
- ADOMD.NET, transactions
- AdomdTransaction object
ms.assetid: 7978c28b-c255-43c0-ad05-f38604d4d8fe
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2b37257b647dc9c1675e36c0f0b6a9b06bbf08d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185089"
---
# <a name="performing-transactions-in-adomdnet"></a>ADOMD.NET에서 트랜잭션 수행
  ADOMD.NET에서는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 개체를 사용하여 지정된 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체의 트랜잭션 컨텍스트를 관리할 수 있습니다. 이 기능을 사용하면 같은 컨텍스트 내에서 여러 명령을 실행할 수 있습니다. 각 명령이 실행되는 동안 읽는 데이터의 변경 없이 각 명령은 같은 데이터를 읽게 됩니다.  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 클래스는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 클래스 라이브러리의 일부이면서 트랜잭션을 지원하는 모든 .NET Framework 데이터 공급자에 의해 구현되는 `System.Data.IDbTransaction` 인터페이스의 구현입니다.  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 개체는 데이터를 읽는 동안 더티 읽기를 방지하기 위해 공유 잠금이 유지되는 커밋된 읽기 트랜잭션만을 지원합니다.  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>을 사용하여 트랜잭션을 시작합니다. 그런 다음 트랜잭션을 사용하기 위해 트랜잭션을 시작한 연결에 대해 명령을 실행합니다. 트랜잭션 작업이 완료되면 트랜잭션을 롤백하거나 커밋할 수 있습니다.  
  
## <a name="starting-a-transaction"></a>트랜잭션 시작  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> 메서드를 호출하여 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체의 인스턴스를 만들 수 있습니다. 다음 예제에서는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 개체의 인스턴스를 만드는 방법을 보여 줍니다.  
  
```  
Dim objTransaction As AdomdTransaction = objConnection.BeginTransaction()  
AdomdTransaction objTransaction = objConnection.BeginTransaction();  
```  
  
## <a name="rolling-back-a-transaction"></a>트랜잭션 롤백  
 완료되지 않은 기존 트랜잭션을 롤백하려면 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Rollback%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 메서드를 호출합니다. 완료되지 않은 기존 트랜잭션에 대해 이 메서드를 호출하면 예외가 throw됩니다.  
  
## <a name="committing-a-transaction"></a>트랜잭션 커밋  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> 메서드를 호출하여 트랜잭션을 시작한 후에는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Commit%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> 메서드를 호출하여 트랜잭션을 완료할 수 있습니다. 완료되지 않은 기존 트랜잭션에 대해 이 메서드를 호출하면 예외가 throw됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADOMD.NET에서 연결 설정](connections-in-adomd-net.md)   
 [ADOMD.NET 클라이언트 프로그래밍](adomd-net-client-programming.md)  
  
  