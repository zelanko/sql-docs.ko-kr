---
title: CLR 데이터베이스 개체에서 데이터 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], data access
- routines [CLR integration]
- data access [CLR integration]
- ADO.NET [CLR integration]
- internal data access [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], data access
- managed code [SQL Server], database objects
- .NET Data Access Provider for SQL Server [CLR integration]
- managed code [SQL Server], data access
- SqlClient provider
- in-process data access providers [CLR integration]
ms.assetid: 9a0f4dee-71c1-42e9-a85e-52382807010f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4561c7b8979a919ea144bab6d9b42f722b089e48
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168553"
---
# <a name="data-access-from-clr-database-objects"></a>CLR 데이터베이스 개체에서 데이터 액세스
  공용 언어 런타임 (CLR) 루틴의 인스턴스에 저장 된 데이터에 쉽게 액세스할 수 있습니다 [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] 이 실행 되는 원격 인스턴스에 저장 된 데이터 뿐만 아니라에서. 루틴을 사용하여 액세스할 수 있는 특정 데이터는 해당 코드가 실행 중인 사용자 컨텍스트에 의해 결정됩니다. .NET Framework Data Provider for를 사용 하 여 CLR 데이터베이스 개체 내에서 데이터에 액세스할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관리 되는 클라이언트 및 중간 계층 응용 프로그램에서 데이터입니다. 따라서 클라이언트 및 중간 계층 응용 프로그램에서 ADO.NET 및 `SqlClient`에 대한 지식을 활용할 수 있습니다.  
  
> [!NOTE]  
>  기본적으로 사용자 정의 형식 메서드 및 사용자 정의 함수를 사용하여 데이터 액세스를 수행할 수는 없습니다. UDT(사용자 정의 형식) 메서드 또는 사용자 정의 함수를 사용하여 읽기 전용 데이터에 액세스하려면 `DataAccess` 또는 `SqlMethodAttribute`의 `SqlFunctionAttribute` 속성을 `DataAccessKind.Read`로 설정해야 합니다. 데이터 수정 작업은 UDT 또는 사용자 정의 함수를 통해 수행할 수 없으며 이를 시도할 경우 실행 시에 예외가 throw됩니다.  
  
 이 섹션에서는 CLR 데이터베이스 개체 내에서 데이터에 액세스할 때 특정 기능 및 동작 차이에 대해서만 설명합니다. ADO.NET의 기능에 대한 자세한 내용은 .NET Framework SDK에 포함된 ADO.NET 설명서를 참조하십시오.  
  
 다음 표에서는 이 섹션에서 다루는 항목을 나열합니다.  
  
 [컨텍스트 연결](context-connection.md)  
 SQL Server에 대한 컨텍스트 연결에 대해 설명합니다.  
  
 [연결에 대한 가장 및 자격 증명](impersonation-and-credentials-for-connections.md)  
 연결 및 연결 자격 증명 가장에 대해 설명합니다.  
  
 [ADO.NET에 대한 SQL Server In-Process 전용 확장](../../clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 in-process 전용 `SqlPipe`, `SqlContext`, `SqlTriggerContext` 및 `SqlDataRecord` 개체에 대해 설명합니다.  
  
 [CLR 통합 및 트랜잭션](../../native-client-ole-db-transactions/transactions.md)  
 System.Transactions 네임스페이스에 제공되는 새 트랜잭션 프레임워크가 ADO.NET 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 통합과 통합되는 방법에 대해 설명합니다.  
  
 [CLR 데이터베이스 개체에서 XML 직렬화](../../../database-engine/dev-guide/xml-serialization-from-clr-database-objects.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내에서 데이터베이스 개체의 XML 직렬화 시나리오를 구현하는 방법에 대해 설명합니다.  
  
  
