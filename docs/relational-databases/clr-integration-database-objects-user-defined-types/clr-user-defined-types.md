---
title: CLR 사용자 정의 형식 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- validation [CLR integration]
- types [CLR integration]
- UserDefined serialization format [CLR integration]
- null values [CLR integration]
- serialization
- Native serialization format [CLR integration]
- databases [CLR integration]
- building database objects [CLR integration], user-defined types
- user-defined types [CLR integration]
- common language runtime [SQL Server], user-defined types
- UDTs [CLR integration]
- database objects [CLR integration], user-defined types
- turning on CLR functionality
- customizing UDT expression return types [CLR integration]
- UDTs [CLR integration], about UDTs
- comparing UDT values
- annotations [CLR integration]
- user-defined types [CLR integration], about UDTs
- variables [CLR integration]
- invoking UDT methods
- indexes [CLR integration]
ms.assetid: 27c4889b-c543-47a8-a630-ad06804f92df
author: rothja
ms.author: jroth
ms.openlocfilehash: 2078b11b44232b44e94191c07fca91998f2c1172
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028354"
---
# <a name="clr-user-defined-types"></a>CLR 사용자 정의 형식
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 .NET Framework CLR (공용 언어 런타임)에서 생성 된 어셈블리에 대해 프로그래밍 된 데이터베이스 개체를 만들 수 있는 기능을 제공 합니다. CLR에서 제공하는 풍부한 프로그래밍 모델을 활용할 수 있는 데이터베이스 개체에는 트리거, 저장 프로시저, 함수, 집계 함수 및 형식이 있습니다.  
  
> [!NOTE]  
>  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 CLR 코드 실행 기능은 기본적으로 OFF로 설정되어 있습니다. **Sp_configure** 시스템 저장 프로시저를 사용 하 여 CLR을 사용 하도록 설정할 수 있습니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 udt (사용자 정의 형식)를 사용 하 여 서버의 스칼라 형식 시스템을 확장 함으로써 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 CLR 개체를 저장할 수 있습니다. UDT에는 여러 요소와 동작이 포함될 수 있어, 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식으로 구성된 일반적인 별칭 데이터 형식과 차별화됩니다.  
  
 UDT는 시스템 전체에서 액세스하므로 복잡한 데이터 형식을 사용하면 성능이 저하될 수 있습니다. 복잡한 데이터는 일반적인 행과 테이블을 사용하여 모델링하는 것이 효율적입니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 UDT는 다음에 적합합니다.  
  
-   날짜, 시간, 통화 및 확장된 숫자 형식  
  
-   지형 공간 애플리케이션  
  
-   인코딩 또는 암호화된 데이터  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 UDT를 개발하는 프로세스는 다음 단계로 구성됩니다.  
  
1.  **UDT를 정의하는 어셈블리를 코딩 및 작성합니다.** UDT는 검증할 수 있는 코드를 생성하는 .NET Framework CLR(공용 언어 런타임)에서 지원하는 모든 언어를 사용하여 정의합니다. 이러한 언어에는 Visual C# 및 Visual Basic .NET 등이 있습니다. 데이터는 .NET Framework 클래스 또는 구조의 필드와 속성으로 노출되며 동작은 클래스 또는 구조의 메서드로 정의됩니다.  
  
2.  **어셈블리를 등록합니다.** 데이터베이스 프로젝트에서 Visual Studio 사용자 인터페이스를 통해 UDT를 배포하거나, 클래스 또는 구조가 포함된 어셈블리를 데이터베이스에 복사하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY 문을 사용하여 UDT를 배포할 수 있습니다.  
  
3.  **SQL Server에서 UDT를 만듭니다.** 어셈블리가 호스트 데이터베이스에 로드되고 나면 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE 문을 사용하여 UDT를 만들고, 클래스 또는 구조의 멤버를 UDT의 멤버로 표시합니다. UDT는 단일 데이터베이스의 컨텍스트에만 있으며, 등록된 후에는 UDT를 만들 때 사용된 외부 파일에 대한 종속 관계가 없습니다.  
  
    > [!NOTE]  
    >  
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이전에는 .NET Framework 어셈블리에서 만든 UDT가 지원되지 않았습니다. 그러나 sp_addtype를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 별칭 데이터 형식을 계속 사용할 **** 수 있습니다. CREATE TYPE 구문은 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 정의 데이터 형식과 UDT를 만드는 데 모두 사용할 수 있습니다.  
  
4.  **UDT를 사용 하 여 테이블, 변수 또는 매개 변수 만들기** [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 사용자 정의 형식은 테이블의 열 정의, [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리의 변수 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수나 저장 프로시저의 인수로 사용 될 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [사용자 정의 형식 만들기](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
 UDT를 만드는 방법에 대해 설명합니다.  
  
 [SQL Server의 사용자 정의 형식 등록](../../relational-databases/clr-integration-database-objects-user-defined-types/registering-user-defined-types-in-sql-server.md)  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 UDT를 등록하고 관리하는 방법에 대해 설명합니다.  
  
 [SQL 서버의 사용자 정의 형식 작업](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
 UDT를 사용하여 쿼리를 만드는 방법에 대해 설명합니다.  
  
 [ADO.NET의 사용자 정의 형식 액세스](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-in-ado-net.md)  
 ADO.NET의 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하여 UDT 작업을 수행하는 방법에 대해 설명합니다.  
  
  
