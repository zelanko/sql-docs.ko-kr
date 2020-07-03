---
title: CLR 데이터베이스 개체에서 데이터 액세스 | Microsoft Docs
description: CLR 루틴은 SQL Server에 대 한 .NET Framework Data Provider (SqlClient 라고도 함)를 사용 하 여 CLR 데이터베이스 개체 내에서 데이터에 액세스할 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 3f89fa45ce0ca73d3406a87c7739ce6e7d777918
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85887827"
---
# <a name="data-access-from-clr-database-objects"></a>CLR 데이터베이스 개체에서 데이터 액세스
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  CLR (공용 언어 런타임) 루틴은 실행 되는 인스턴스에 저장 된 데이터 뿐만 아니라 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 원격 인스턴스에 저장 된 데이터에 쉽게 액세스할 수 있습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . 루틴을 사용하여 액세스할 수 있는 특정 데이터는 해당 코드가 실행 중인 사용자 컨텍스트에 의해 결정됩니다. 의 .NET Framework Data Provider (SqlClient 라고도 함)를 사용 하 여 CLR 데이터베이스 개체 내에서 데이터에 액세스할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 수 있습니다. **SqlClient** 이 공급자는 관리 클라이언트 및 중간 계층 애플리케이션에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터에 액세스하는 개발자가 사용하는 것과 동일한 공급자입니다. 이로 인해 클라이언트 및 중간 계층 응용 프로그램에서 ADO.NET 및 **SqlClient** 에 대 한 지식을 활용할 수 있습니다.  
  
> [!NOTE]  
>  기본적으로 사용자 정의 형식 메서드 및 사용자 정의 함수를 사용하여 데이터 액세스를 수행할 수는 없습니다. **SqlMethodAttribute** 또는 **SqlFunctionAttribute** 의 **DataAccess** 속성을 **dataaccesskind.read** 로 설정 하 여 UDT (사용자 정의 형식) 메서드나 사용자 정의 함수에서 읽기 전용 데이터 액세스를 사용 하도록 설정 해야 합니다. 데이터 수정 작업은 UDT 또는 사용자 정의 함수를 통해 수행할 수 없으며 이를 시도할 경우 실행 시에 예외가 throw됩니다.  
  
 이 섹션에서는 CLR 데이터베이스 개체 내에서 데이터에 액세스할 때 특정 기능 및 동작 차이에 대해서만 설명합니다. ADO.NET의 기능에 대한 자세한 내용은 .NET Framework SDK에 포함된 ADO.NET 설명서를 참조하십시오.  
  
 다음 표에서는 이 섹션에서 다루는 항목을 나열합니다.  
  
 [컨텍스트 연결](../../../relational-databases/clr-integration/data-access/context-connection.md)  
 SQL Server에 대한 컨텍스트 연결에 대해 설명합니다.  
  
 [연결에 대한 가장 및 자격 증명](../../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
 연결 및 연결 자격 증명 가장에 대해 설명합니다.  
  
 [ADO.NET에 대한 SQL Server In-Process 전용 확장](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 In-process 관련 **SqlPipe**, **sqlcontext**, **sqltriggercontext**및 **SqlDataRecord** 개체에 대해 설명 합니다.  
  
 [CLR 통합 및 트랜잭션](../../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
 System.Transactions 네임스페이스에 제공되는 새 트랜잭션 프레임워크가 ADO.NET 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 통합과 통합되는 방법에 대해 설명합니다.  
  
 [CLR 데이터베이스 개체에서 XML 직렬화](https://msdn.microsoft.com/library/ac84339b-9384-4710-bebc-01607864a344)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내에서 데이터베이스 개체의 XML 직렬화 시나리오를 구현하는 방법에 대해 설명합니다.  
  
  
