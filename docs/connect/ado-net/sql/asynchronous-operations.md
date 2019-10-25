---
title: 비동기 작업
description: .NET Framework에서 비동기 모델을 사용한 후 모델링되는 API를 사용하여 비동기 데이터베이스 작업을 수행하는 방법을 설명합니다.
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 79cde936328476408fabb3df7a6bff8d983ace1c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452326"
---
# <a name="asynchronous-operations"></a>비동기 작업

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

명령 실행과 같은 일부 데이터베이스 작업을 완료 하는 데 상당한 시간이 걸릴 수 있습니다. 이 경우 단일 스레드 응용 프로그램은 다른 작업을 차단 하 고 명령이 완료 될 때까지 기다려야 자체 작업을 계속할 수 있습니다. 반면에 장기 실행 작업을 백그라운드 스레드에 할당할 수 있으면 작업을 마칠 때까지 포그라운드 스레드를 활성 상태로 유지할 수 있습니다. 예를 들어 Windows 응용 프로그램에서 장기 실행 작업을 백그라운드 스레드에 위임 하면 작업이 실행 되는 동안 사용자 인터페이스 스레드가 응답성을 유지할 수 있습니다.  
  
.NET에서는 개발자가 백그라운드 스레드를 활용 하 고 사용자 인터페이스나 우선 순위가 높은 스레드를 사용 하 여 <xref:Microsoft.Data.SqlClient.SqlCommand> 클래스에서 다른 작업을 완료 하는 데 사용할 수 있는 몇 가지 표준 비동기 디자인 패턴을 제공 합니다. 특히 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> 및 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A> 메서드와 쌍을 이루는 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 및 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 메서드는 비동기 지원을 제공 합니다.  
  
> [!NOTE]
>  비동기 프로그래밍은 .NET의 핵심 기능입니다. 개발자에 게 제공 되는 다양 한 비동기 기술에 대 한 자세한 내용은 [동기 메서드를 비동기적으로 호출](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)을 참조 하세요.  
  
ADO.NET 기능을 사용 하는 비동기 기술을 사용 하는 경우에는 특별 한 고려 사항이 추가 되지 않지만 다중 스레드 응용 프로그램을 만들 때의 이점과 문제를 파악 하는 것이 중요 합니다. 이 섹션에 나오는 예제에서는 다중 스레드 기능을 통합 하는 응용 프로그램을 빌드할 때 개발자가 고려해 야 하는 몇 가지 중요 한 문제를 설명 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
[콜백을 사용하는 Windows 애플리케이션](windows-applications-callbacks.md)  
비동기 명령을 안전 하 게 실행 하는 방법을 보여 주는 예제를 제공 합니다 .이 예제에서는 별도의 스레드에서 폼과 해당 콘텐츠를 사용 하 여 상호 작용을 올바르게 처리 합니다.  
  
[대기 핸들을 사용하는 ASP.NET 애플리케이션](aspnet-apps-use-wait-handles.md)  
모든 명령이 완료 될 때 대기 핸들을 사용 하 여 작업을 관리 하는 ASP.NET 페이지에서 여러 동시 명령을 실행 하는 방법을 보여 주는 예제를 제공 합니다.  
  
[콘솔 애플리케이션에서 폴링](poll-console-applications.md)  
폴링을 사용 하 여 콘솔 응용 프로그램에서 비동기 명령 실행이 완료 될 때까지 대기 하는 방법을 보여 주는 예제를 제공 합니다. 이 기술은 클래스 라이브러리나 사용자 인터페이스가 없는 다른 응용 프로그램 에서도 유효 합니다.  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
- [비동기 비동기 메서드 호출](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)
