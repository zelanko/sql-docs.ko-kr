---
description: SMO 프로그램 만들기
title: SMO 프로그램 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SMO [SQL Server], programming
ms.assetid: 7d2f0bcf-f1ae-45b8-bc3f-7aea4fae7e45
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 00ae0e27bb4d90c286ef1b199c200ab5b900f706
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467264"
---
# <a name="creating-smo-programs"></a>SMO 프로그램 만들기
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  SMO([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects) 개체의 일반적인 프로그래밍에는 메서드 실행, 속성 설정 및 컬렉션 조작과 같이 모든 개체가 공유하는 공통적인 영역이 포함됩니다.  
  
|항목|설명|  
|-----------|-----------------|  
|[SQL Server 인스턴스에 연결](../../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 연결을 설정하는 가장 기본적인 SMO 프로그램입니다. Windows 인증과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 수행하는 방법을 보여 줍니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 로컬 및 원격 인스턴스에 연결하는 방법을 보여 주는 예제도 포함되어 있습니다.|  
|[SQL Server 인스턴스에서 연결 끊기](../../../relational-databases/server-management-objects-smo/create-program/disconnecting-from-an-instance-of-sql-server.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 끊는 방법을 보여 주는 프로그램입니다.|  
|[메서드 호출](../../../relational-databases/server-management-objects-smo/create-program/calling-methods.md)|이 섹션에서는 일반적인 메서드 호출 방법을 설명합니다. 매개 변수를 사용하는 방법과 <xref:System.Data.DataTable> 개체에 반환된 데이터 테이블을 처리하는 방법을 보여 줍니다. 또한 개체 생성자를 호출 하는 방법 및 **Clone** 메서드를 호출 하는 방법에 대 한 예제를 제공 합니다.|  
|[속성 설정 - SMO](../../../relational-databases/server-management-objects-smo/create-program/setting-properties-smo.md)|이 섹션에서는 여러 가지 유형의 속성을 설정하는 방법을 설명합니다. 개체 속성을 설정하고 얻는 방법을 보여 주며, 개체가 생성될 때 개체 속성을 설정하는 예와 개체의 모든 속성을 대상으로 반복을 수행하는 방법도 포함되어 있습니다.|  
|[컬렉션 사용](../../../relational-databases/server-management-objects-smo/create-program/using-collections.md)|개체 컬렉션에 사용되는 기법에 대해 설명하는 여러 프로그램이 포함되어 있습니다. 컬렉션을 사용하여 개체를 참조하는 방법을 보여 줍니다. 컬렉션의 멤버를 대상으로 반복을 수행하는 방법에 대한 예도 포함되어 있습니다.|  
|[SMO 이벤트 처리](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-events.md)|이 섹션에서는 SMO에서 이벤트를 설정하고 처리하는 방법을 설명합니다. 이벤트 처리기를 설정하는 방법과 이벤트 구독을 설정하는 방법에 대한 예가 포함되어 있습니다.|  
|[SMO 예외 처리](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-exceptions.md)|이 섹션에서는 SMO에서 예외를 트래핑하는 방법을 설명합니다. 예외를 포착하는 방법과 내부 예외를 표시하는 방법에 대한 예가 포함되어 있습니다.|  
|[데이터 형식 사용](../../../relational-databases/server-management-objects-smo/create-program/working-with-data-types.md)|이 섹션에서는 여러 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 사용하는 방법에 대해 설명합니다. 개체 생성자의 사양으로 데이터 형식을 구성하는 방법을 설명합니다. 기본 생성자를 사용하여 데이터 형식을 만드는 방법에 대한 예도 포함되어 있습니다.|  
|[트랜잭션 사용](../../../relational-databases/server-management-objects-smo/create-program/using-transactions.md)|이 섹션에서는 SMO 프로그램에서 트랜잭션 처리를 구현하는 방법을 설명합니다. SMO 프로그램에서 트랜잭션을 사용하는 방법에 대한 예가 포함되어 있습니다.|  
|[캡처 모드 사용](../../../relational-databases/server-management-objects-smo/create-program/using-capture-mode.md)|이 섹션에서는 SMO 프로그램의 출력을 기록하는 방법을 설명합니다. 예에서는 SMO 프로그램을 나중에 실행하기 위해 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 인스턴스에 전송된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 문으로 기록합니다.|  
  
  
