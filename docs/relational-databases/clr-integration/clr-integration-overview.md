---
title: CLR 통합 개요 | 마이크로 소프트 문서
description: CLR을 호스팅하는 Microsoft SQL Server를 CLR 통합이라고 합니다. 관리 코드를 작성하면 성능이 향상될 수 있습니다. SQL Server는 CAS를 사용하여 관리되는 코드를 보호합니다.
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], about CLR integration
- extended stored procedures [SQL Server], vs. managed code
- objects [CLR integration]
- Transact-SQL vs. managed code
- managed code [SQL Server], vs. Transact-SQL
- managed code [SQL Server], vs. extended stored procedures
- execution at client vs. execution at server [CLR integration]
ms.assetid: 5aa176da-3652-4afa-a742-4c40c77ce5c3
author: rothja
ms.author: jroth
ms.openlocfilehash: 64c30629cf7608a7816ec16c458f55f4dfad1e75
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488110"
---
# <a name="clr-integration---overview"></a>CLR 통합 - 개요
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  CLR(공용 언어 런타임)은 Microsoft .NET Framework의 핵심으로, 모든 .NET Framework 코드의 실행 환경을 제공합니다. CLR 내에서 실행되는 코드를 관리 코드라고 합니다. CLR은 JIT(Just-In-Time) 컴파일, 메모리 할당 및 관리, 형식 안전성 적용, 예외 처리, 스레드 관리, 보안을 비롯하여 프로그램 실행에 필요한 다양한 기능과 서비스를 제공합니다.  자세한 내용은 .NET Framework SDK를 참조하십시오.  
  
 Microsoft SQL Server에 호스팅된 CLR(CLR 통합이라고 함)을 사용하면 관리 코드로 저장 프로시저, 트리거, 사용자 정의 함수, 사용자 정의 형식 및 사용자 정의 집계를 작성할 수 있습니다. 관리 코드는 실행 전에 네이티브 코드로 컴파일되므로 일부 시나리오에서 성능이 훨씬 향상될 수 있습니다.  
  
 관리 코드는 CAS(Code Access Security)를 사용하여 어셈블리에서 특정 작업을 수행할 수 없도록 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CAS를 사용하여 관리 코드의 보안을 유지하고 운영 체제나 데이터베이스 서버의 손상을 방지합니다.  
  
## <a name="advantages-of-clr-integration"></a>CLR 통합의 장점  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 특히 데이터베이스의 데이터에 직접 액세스하고 조작할 수 있도록 설계되었습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]은 데이터 액세스 및 관리 기능이 뛰어나지만 모든 기능을 갖춘 프로그래밍 언어는 아닙니다. 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 배열, 컬렉션, for-each 루프, 비트 시프트 또는 클래스를 지원하지 않습니다. 이러한 구문 중 일부는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 시뮬레이션할 수 있지만 관리 코드에 해당 구문에 대한 통합 지원이 있습니다. 시나리오에 따라 이러한 기능을 위해 특정 데이터베이스 기능을 관리 코드로 구현해야 할 수 있습니다.  
  
 Microsoft Visual Basic .NET 및 Microsoft Visual C#은 캡슐화, 상속 및 다형성과 같은 개체 지향 기능을 제공합니다. 이제 관련된 코드를 클래스와 네임스페이스로 쉽게 구성할 수 있으므로 많은 서버 코드에서 작업하는 경우 코드를 쉽게 구성하고 유지 관리할 수 있습니다.  
  
 관리 코드는 [!INCLUDE[tsql](../../includes/tsql-md.md)]보다 계산 및 복잡한 실행 논리에 더 적합하며, 문자열 처리 및 정규식을 비롯한 많은 복잡한 태스크에 대한 광범위한 지원을 제공합니다. .NET Framework 라이브러리에 있는 기능을 사용하여 수천 개의 미리 작성된 클래스와 루틴에 액세스할 수 있습니다. 임의의 저장 프로시저, 트리거 또는 사용자 정의 함수에서 쉽게 액세스할 수 있습니다. BCL(기본 클래스 라이브러리)에는 문자열 조작, 고급 수학 연산, 파일 액세스, 암호화 등에 대한 기능을 제공하는 클래스가 포함되어 있습니다.  
  
> [!NOTE]  
>  이러한 클래스는 대부분 SQL Server의 CLR 코드 내에서 사용할 수 있지만 서버측 사용에 적합하지 않은 클래스(예: 창 작업 클래스)는 사용할 수 없습니다. 자세한 내용은 [Supported .NET Framework Libraries](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)을 참조하세요.  
  
 관리 코드의 이점 중 하나는 코드가 잘 정의된 허용 가능한 방식으로만 형식에 액세스하도록 하는 형식 안전성입니다. 관리 코드가 실행되기 전에 CLR에서 해당 코드가 안전한지 확인합니다. 예를 들어 코드를 검사하여 이전에 기록되지 않은 메모리를 읽지 않도록 합니다. CLR은 코드가 관리되지 않는 메모리를 조작하지 않도록 하는 데에도 유용합니다.  
  
 CLR 통합은 잠재적 성능 향상을 제공합니다. 자세한 내용은 [CLR 통합 성능을](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)참조하십시오.  
 
> [!WARNING]
>  CLR은 더 이상 보안 경계로 지원되지 않는 .NET Framework의 CAS(코드 액세스 보안)를 사용합니다. `PERMISSION_SET = SAFE`로 만든 CLR 어셈블리에서 외부 시스템 리소스에 액세스하고, 비관리 코드를 호출하고, sysadmin 권한을 얻을 수 있습니다. [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]부터 CLR 어셈블리의 보안을 강화하기 위해 `clr strict security`라는 `sp_configure` 옵션이 도입되었습니다. `clr strict security`는 기본적으로 사용되며 `SAFE` 및 `EXTERNAL_ACCESS` 어셈블리가 `UNSAFE`로 표시된 것처럼 처리됩니다. `clr strict security` 옵션은 이전 버전과의 호환성을 위해 사용하지 않도록 설정할 수 있지만 권장하지는 않습니다. 모든 어셈블리는 master 데이터베이스에서 `UNSAFE ASSEMBLY` 권한이 부여된 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명하는 것이 좋습니다. 자세한 내용은 [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md)를 참조하세요. 
  
## <a name="choosing-between-transact-sql-and-managed-code"></a>Transact-SQL 및 관리 코드 선택  
 저장 프로시저, 트리거 및 사용자 정의 함수를 작성하는 경우 일반적인 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용할지 또는 Visual Basic .NET 또는 Visual C#과 같은 .NET Framework 언어를 사용할지 결정해야 합니다. 거의 또는 전혀 절차적 논리 없이 코드에서 대체로 데이터 액세스를 수행하는 경우에 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용합니다. 복잡한 논리를 제공하는 CPU 사용량이 많은 함수 및 프로시저의 경우나 .NET Framework의 BCL을 이용하려는 경우에 관리 코드를 사용합니다.  
  
### <a name="choosing-between-execution-in-the-server-and-execution-in-the-client"></a>서버에서 실행 및 클라이언트에서 실행 선택  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 관리 코드를 사용할지 결정할 때 고려되는 또 다른 요소는 코드를 배치할 위치(서버 컴퓨터 또는 클라이언트 컴퓨터)입니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 관리 코드는 모두 서버에서 실행할 수 있습니다. 이 경우 코드와 데이터가 더 가까이 있고 서버의 처리 능력을 이용할 수 있습니다. 반면, 프로세서를 많이 사용하는 태스크를 데이터베이스 서버에 배치하는 것은 피하는 것이 좋습니다. 현재 대부분의 클라이언트 컴퓨터는 매우 강력하며, 가능한 한 많은 코드를 클라이언트에 배치하여 이 처리 능력을 이용할 수도 있습니다. 관리 코드는 클라이언트 컴퓨터에서 실행할 수 있지만 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 실행할 수 없습니다.  
  
## <a name="choosing-between-extended-stored-procedures-and-managed-code"></a>확장 저장 프로시저 및 관리 코드 선택  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저로는 수행할 수 없는 기능을 수행하도록 확장 저장 프로시저를 작성할 수 있습니다. 하지만 형식 안전성이 확인된 관리 코드와 달리 확장 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스의 무결성을 손상시킬 수 있습니다. 또한 메모리 관리, 스레드 및 파이버 예약, 동기화 서비스 등이 CLR의 관리 코드와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간에 보다 강력하게 통합되어 있습니다. CLR 통합을 사용하면 확장 저장 프로시저보다 안전한 방식으로 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 불가능한 태스크를 수행하는 데 필요한 저장 프로시저를 작성할 수 있습니다. CLR 통합 및 확장 된 저장 프로시저에 대 한 자세한 내용은 [CLR 통합의 성능](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)참조  
  
## <a name="see-also"></a>참고 항목  
 [.NET 프레임워크 설치](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [CLR 통합아키텍처](https://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9)   
 [CLR 데이터베이스 개체의 데이터 액세스](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CLR 통합으로 작업 시작](../../relational-databases/clr-integration/database-objects/getting-started-with-clr-integration.md)  
  
  
