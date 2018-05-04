---
title: .NET Framework 라이브러리를 지원 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 24cd0f69a0167b5e742381b0e2e88f2cc84d1a2c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="supported-net-framework-libraries"></a>지원되는 .NET Framework 라이브러리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 호스팅된 CLR(공용 언어 런타임)을 사용하면 관리되는 코드로 저장 프로시저, 트리거, 사용자 정의 함수, 사용자 정의 형식 및 사용자 정의 집계를 작성할 수 있습니다. .NET Framework 클래스 라이브러리에 있는 기능을 사용하면 문자열 조작, 고급 수학 연산, 파일 액세스, 암호화 등에 대한 기능을 제공하는 미리 작성된 클래스에 액세스할 수 있습니다. 임의의 관리되는 저장 프로시저, 사용자 정의 형식, 트리거, 사용자 정의 함수 또는 사용자 정의 집계에서 이러한 클래스에 액세스할 수 있습니다.  
  
> [!NOTE]  
>  GAC(전역 어셈블리 캐시)에서 지원되지 않는 어셈블리를 서비스 또는 업그레이드하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 응용 프로그램 작동이 중지될 수 있습니다. 이는 GAC의 라이브러리를 제공하거나 업그레이드할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부의 어셈블리는 업데이트되지 않기 때문입니다. 어셈블리가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스와 GAC에 모두 포함되어 있는 경우 해당 어셈블리의 두 복사본이 정확하게 일치해야 합니다. 일치하지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 통합에서 해당 어셈블리를 사용할 때 오류가 발생합니다. 서비스 또는 지원 되지 않는.NET Framework 어셈블리를 포함 하 여 데이터베이스에도 등록 된 GAC의 어셈블리를 업그레이드 하는 경우 서비스 또는 업그레이드 내부의 어셈블리 복사본에 있는지 확인 프로그램 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에  **ALTER ASSEMBLY** 문. 자세한 내용은 [기술 자료 문서 949080](http://support.microsoft.com/kb/949080)을 참조하십시오.  
  
## <a name="supported-libraries"></a>지원되는 라이브러리  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에는 테스트를 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와의 상호 작용에 대한 안정성 및 보안 표준을 충족하는 것이 확인된 지원되는 .NET Framework 라이브러리 목록이 포함되어 있습니다. 지원되는 라이브러리는 서버에 명시적으로 등록하지 않고도 코드에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 GAC(전역 어셈블리 캐시)에서 직접 해당 라이브러리를 로드합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 CLR 통합에서 지원되는 라이브러리/네임스페이스는 다음과 같습니다.  
  
-   CustomMarshalers  
  
-   Microsoft.VisualBasic  
  
-   Microsoft.VisualC  
  
-   mscorlib  
  
-   시스템  
  
-   System.Configuration  
  
-   System.Data  
  
-   System.Data.OracleClient  
  
-   System.Data.SqlXml  
  
-   System.Deployment  
  
-   System.Security  
  
-   System.Transactions  
  
-   System.Web.Services  
  
-   System.Xml  
  
-   System.Core.dll  
  
-   System.Xml.Linq.dll  
  
## <a name="unsupported-libraries"></a>지원되지 않는 라이브러리  
 지원되지 않는 라이브러리도 관리되는 저장 프로시저, 트리거, 사용자 정의 함수, 사용자 정의 형식 및 사용자 정의 집계에서 호출할 수 있습니다. 지원 되지 않는 라이브러리에 먼저 등록 되어야 합니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스를 사용 하는 **CREATE ASSEMBLY** 문, 코드에서 사용할 수 있습니다. 지원되지 않는 라이브러리를 서버에 등록하고 실행하는 경우 보안과 안정성을 검토하여 테스트해야 합니다.  
  
 예를 들어는 **System.DirectoryServices** 네임 스페이스는 지원 되지 않습니다. System.DirectoryServices.dll 어셈블리를 등록 해야 **UNSAFE** 사용 권한 사용자 코드에서 호출할 수 있습니다. **UNSAFE** 권한에 필요 하기 때문에 있는 클래스는 **System.DirectoryServices** 네임 스페이스에 대 한 요구 사항을 충족 하지 않는 **안전 하 게 보호** 또는  **EXTERNAL_ACCESS**합니다. 자세한 내용은 참조 [CLR 통합 프로그래밍 모델 제한 사항](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) 및 [CLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [어셈블리 만들기](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [CLR 통합 코드 액세스 보안](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 통합 프로그래밍 모델 제한 사항](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
