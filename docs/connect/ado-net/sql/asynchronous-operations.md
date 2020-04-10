---
title: 비동기 작업
description: .NET Framework에서 비동기 모델을 사용한 후 모델링되는 API를 사용하여 비동기 데이터베이스 작업을 수행하는 방법을 설명합니다.
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 4c88a8ccbc242b0fd85c66acfb3539ec260c58dd
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928934"
---
# <a name="asynchronous-operations"></a>비동기 작업

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

명령 실행과 같은 일부 데이터베이스 작업을 완료하는 데 상당한 시간이 걸릴 수 있습니다. 그런 경우 단일 스레드 애플리케이션에서는 다른 작업을 차단하고 명령이 완료될 때까지 대기한 다음 다른 작업을 계속해야 합니다. 반면에 장기 실행 작업을 백그라운드 스레드에 할당할 수 있으면 작업을 마칠 때까지 포그라운드 스레드를 활성 상태로 유지할 수 있습니다. 예를 들어 Windows 애플리케이션에서 장기 실행 작업을 백그라운드 스레드에 위임하면 작업이 실행되는 동안 사용자 인터페이스 스레드가 응답성을 유지할 수 있습니다.  
  
.NET에서는 개발자가 백그라운드 스레드를 활용하고 사용자 인터페이스 또는 우선 순위가 높은 스레드를 확보하여 <xref:Microsoft.Data.SqlClient.SqlCommand> 클래스에서 다른 작업을 완료하는 데 사용할 수 있는 몇 가지 표준적인 비동기 디자인 패턴을 제공합니다. 특히 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 및 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 메서드와 쌍을 이루는 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> 및 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A> 메서드는 비동기 지원을 제공합니다.  
  
> [!NOTE]
>  비동기 프로그래밍은 .NET의 핵심 기능입니다. 개발자에게 제공되는 다양한 비동기 기술에 대한 자세한 내용은 [비동기적으로 동기 메서드 호출](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)을 참조하세요.  
  
ADO.NET 기능을 사용하는 비동기 기술을 사용하는 경우에는 특별한 고려 사항이 추가되지 않지만 다중 스레드 애플리케이션을 만들 때의 이점과 위험을 파악하는 것이 중요합니다. 이 섹션에 나오는 예제에서는 다중 스레드 기능을 통합하는 애플리케이션을 빌드할 때 개발자가 고려해야 하는 몇 가지 중요한 문제를 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
[콜백을 사용하는 Windows 애플리케이션](windows-applications-callbacks.md)  
비동기 명령을 안전하게 실행하는 방법을 보여 주는 예제를 제공합니다. 이 예제에서는 별도의 스레드에서 양식과 해당 내용을 사용하여 상호 작용을 올바르게 처리합니다.  
  
[대기 핸들을 사용하는 ASP.NET 애플리케이션](aspnet-apps-use-wait-handles.md)  
모든 명령이 완료될 때 대기 핸들로 작업을 관리해 ASP.NET 페이지의 동시 명령을 어떻게 실행할 수 있을지를 예제로 시연합니다.  
  
[콘솔 애플리케이션에서 폴링](poll-console-applications.md)  
폴링을 사용하여 콘솔 애플리케이션에서 비동기 명령 실행이 완료될 때까지 대기하는 방법을 보여주는 예제를 제공합니다. 이 기술은 클래스 라이브러리나 사용자 인터페이스가 없는 다른 애플리케이션에서도 유효합니다.  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
- [비동기적으로 동기 메서드 호출](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)
