---
title: 연결 설정
description: SqlClient 공급자가 SQL Server에 연결하기 위한 지침입니다.
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 3af512f3-87d9-4005-9e2f-abb1060ff43f
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 2eb3c7d996463b9c581ea60bc11f853a5d131582
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419752"
---
# <a name="establishing-connection"></a>연결 설정

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SQL Server에 연결하려면 Microsoft SqlClient Data Provider for SQL Server의 <xref:Microsoft.Data.SqlClient.SqlConnection> 개체를 사용합니다. 연결 문자열을 안전하게 저장하고 검색하려면 [연결 정보 보호](protecting-connection-information.md)를 참조하세요.

## <a name="closing-connections"></a>연결 닫기

사용이 끝나면 해당 연결이 풀로 반환되도록 닫아 두는 것이 좋습니다. Visual Basic 또는 C#의 `Using` 블록은 처리되지 않은 예외가 발생하더라도 코드에 블록이 있으면 연결을 자동으로 제거합니다. 자세한 내용은 [using 문](/dotnet/docs/csharp/language-reference/keywords/using-statement.md) 및 [Using 문](/dotnet/docs/visual-basic/language-reference/statements/using-statement.md)을 참조하세요.

연결 개체의 `Close` 또는 `Dispose` 메소드를 사용할 수도 있습니다. 명시적으로 닫히지 않은 연결은 풀에 추가되거나 반환되지 않을 수 있습니다. 예를 들어, 범위를 벗어났지만 명시적으로 닫히지 않은 연결은 최대 풀 크기에 도달했으며 여전히 유효한 경우에만 연결 풀로 반환됩니다.

> [!NOTE]
> 클래스의 `Finalize` 메소드에 있는 **Connection**, **DataReader** 또는 기타 관리 개체에서 `Close` 또는 `Dispose`를 호출하지 마세요. 종료자에서는 클래스에 직접 속한 관리되지 않는 리소스만 해제합니다. 클래스에 관리되지 않는 리소스가 없는 경우 클래스 정의에 `Finalize` 메서드를 포함하지 마세요. 자세한 내용은 [가비지 수집](/dotnet/docs/standard/garbage-collection/index.md)을 참조하세요.

> [!NOTE]
> 연결이 연결 풀에서 반환될 경우에는 실제로 해제된 것이 아니므로 연결이 연결 풀에서 반입되거나 연결 풀로 반환되는 경우 서버에서 로그인 및 로그아웃 이벤트가 발생하지 않습니다. 자세한 내용은 [SQL Server 연결 풀링(ADO.NET)](sql-server-connection-pooling.md)을 참조하세요.

## <a name="connecting-to-sql-server"></a>SQL Server에 연결

유효한 문자열 형식 이름 및 값은 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> 개체의 <xref:Microsoft.Data.SqlClient.SqlConnection> 속성을 참조하세요. <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> 클래스를 사용하여 런타임에 구문상 유효한 연결 문자열을 만들 수도 있습니다. 자세한 내용은 [연결 문자열 작성기](connection-string-builders.md)를 참조하세요.

다음 코드 예제에서는 SQL Server 데이터베이스에 대해 연결을 만들어 여는 방법을 보여 줍니다.

[!code-csharp[SqlConnection.Open#1](~/../sqlclient/doc/samples/SqlConnection_Open.cs#1)]

### <a name="integrated-security-and-aspnet"></a>통합 보안 및 ASP.NET

SQL Server 통합 보안(신뢰할 수 있는 연결이라고도 함)은 연결 문자열에 사용자 ID와 암호를 노출하지 않고 연결 인증에 권장되는 방법이므로 SQL Server에 연결할 때 보호 기능을 제공합니다. 통합 보안에서는 실행 중인 프로세스의 현재 보안 ID, 즉 토큰을 사용합니다. 데스크톱 애플리케이션의 경우 이 ID는 일반적으로 현재 로그온한 사용자의 ID입니다.

ASP.NET 애플리케이션의 보안 ID는 여러 가지 서로 다른 옵션 중 하나로 설정할 수 있습니다. ASP.NET 애플리케이션에서 SQL Server에 연결할 때 사용하는 보안 ID에 대한 자세한 내용은 [ASP.NET 가장](/previous-versions/aspnet/xh507fc5(v=vs.100)), [ASP.NET 인증](/previous-versions/aspnet/eeyk640h(v=vs.100)) 및 [방법: Windows 통합 보안을 사용하여 SQL Server에 액세스](/previous-versions/aspnet/bsz5788z(v=vs.100))를 참조하세요.

## <a name="see-also"></a>참고 항목

- [데이터 원본에 연결](connecting-to-data-source.md)
- [연결 문자열](connection-strings.md)
