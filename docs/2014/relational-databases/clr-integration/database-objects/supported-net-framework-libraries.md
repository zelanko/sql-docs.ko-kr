---
title: .NET Framework 라이브러리를 지원 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1e24738e82e9e73c5777780377207fdc4471aa47
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187421"
---
# <a name="supported-net-framework-libraries"></a>지원되는 .NET Framework 라이브러리
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 호스팅된 CLR(공용 언어 런타임)을 사용하면 관리되는 코드로 저장 프로시저, 트리거, 사용자 정의 함수, 사용자 정의 형식 및 사용자 정의 집계를 작성할 수 있습니다. .NET Framework 클래스 라이브러리에 있는 기능을 사용하면 문자열 조작, 고급 수학 연산, 파일 액세스, 암호화 등에 대한 기능을 제공하는 미리 작성된 클래스에 액세스할 수 있습니다. 임의의 관리되는 저장 프로시저, 사용자 정의 형식, 트리거, 사용자 정의 함수 또는 사용자 정의 집계에서 이러한 클래스에 액세스할 수 있습니다.  
  
> [!NOTE]  
>  서비스 또는 전역 어셈블리 캐시 (GAC)에 지원 되지 않는 어셈블리를 업그레이드 하는 경우 프로그램 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 어셈블리에 모두 포함 되어 있는 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 통합 합니다. 지원되지 않는 .NET Framework 어셈블리를 비롯하여 데이터베이스에도 등록된 GAC의 어셈블리를 서비스 또는 업그레이드하는 경우 `ALTER ASSEMBLY` 문을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스 내의 어셈블리 복사본도 서비스 또는 업그레이드해야 합니다. 자세한 내용은 참조 [기술 자료 문서 949080](http://support.microsoft.com/kb/949080)합니다.  
  
## <a name="supported-libraries"></a>지원되는 라이브러리  
 부터는 [!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)] 와 상호 작용에 대 한 안정성 및 보안 표준에 부합 되는지 확인 하려면 테스트는 지원 되는.NET Framework 라이브러리의 목록이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 직접에서 전역 어셈블리 캐시 (GAC) 미리 로드 합니다.  
  
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
 지원되지 않는 라이브러리도 관리되는 저장 프로시저, 트리거, 사용자 정의 함수, 사용자 정의 형식 및 사용자 정의 집계에서 호출할 수 있습니다. 지원되지 않는 라이브러리는 `CREATE ASSEMBLY` 문을 사용하여 먼저 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 등록해야 코드에서 사용할 수 있습니다. 지원되지 않는 라이브러리를 서버에 등록하고 실행하는 경우 보안과 안정성을 검토하여 테스트해야 합니다.  
  
 예를 들어 `System.DirectoryServices` 네임스페이스는 지원되지 않습니다. `UNSAFE` 권한을 사용하여 System.DirectoryServices.dll 어셈블리를 등록해야 코드에서 호출할 수 있습니다. `UNSAFE` 네임스페이스의 클래스는 `System.DirectoryServices` 또는 `SAFE`에 대한 요구 사항을 충족하지 않으므로 `EXTERNAL_ACCESS` 권한이 필요합니다. 자세한 내용은 참조 [CLR 통합 프로그래밍 모델 제한 사항](clr-integration-programming-model-restrictions.md) 및 [CLR Integration Code Access Security](../security/clr-integration-code-access-security.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [어셈블리 만들기](../assemblies/creating-an-assembly.md)   
 [CLR 통합 코드 액세스 보안](../security/clr-integration-code-access-security.md)   
 [CLR 통합 프로그래밍 모델 제한 사항](clr-integration-programming-model-restrictions.md)  
  
  