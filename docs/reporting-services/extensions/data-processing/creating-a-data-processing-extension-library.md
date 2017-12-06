---
title: "데이터 처리 확장 프로그램 라이브러리 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 82f4b71b-dd39-467d-8d8c-6771eb2b12de
caps.latest.revision: "39"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8765bcb56ffd9b7f081ae9c7363d2a4f47f6ab1c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="creating-a-data-processing-extension-library"></a>데이터 처리 확장 프로그램 라이브러리 만들기
  만드는 각 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램은 고유한 네임스페이스에 할당하고 라이브러리 또는 어셈블리 파일로 만들어야 합니다. 네임스페이스의 정확한 이름은 중요하지 않지만 고유한 이름이어야 하며 다른 확장 프로그램과 공유하면 안 됩니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)]에서는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 포함되어 있는 데이터 처리 확장 프로그램에 대해 <xref:Microsoft.ReportingServices.DataProcessing> 네임스페이스를 사용합니다. 회사의 데이터 처리 확장 프로그램에 대해 고유한 네임스페이스를 만들어야 합니다.  
  
 다음 예는 데이터 처리 인터페이스 및 유틸리티 클래스가 포함된 네임스페이스를 사용하는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 시작하기 위한 코드를 보여 줍니다.  
  
```vb  
Imports System  
Imports Microsoft.ReportingServices.DataProcessing  
Imports Microsoft.ReportingServices.Interfaces  
  
Namespace CompanyName.ExtensionName  
   ...  
```  
  
```csharp  
using System;  
using Microsoft.ReportingServices.DataProcessing;  
using Microsoft.ReportingServices.Interfaces;  
  
namespace CompanyName.ExtensionName  
{  
   ...  
```  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 컴파일할 때 데이터 처리 확장 프로그램 인터페이스가 포함된 Microsoft.ReportingServices.Interfaces.dll에 대한 참조를 컴파일러에 제공해야 합니다. <xref:Microsoft.ReportingServices.DataProcessing> 네임스페이스는 데이터 처리 확장 프로그램 인터페이스를 구현하는 데 필요하고, <xref:Microsoft.ReportingServices.Interfaces> 네임스페이스는 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 인터페이스를 구현하는 데 필요합니다. 예를 들어 C#으로 작성된 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 구현할 코드가 포함된 모든 파일이 확장명 .cs로 단일 디렉터리에 있는 경우 해당 디렉터리에서 다음 명령을 실행하여 CompanyName.ExtensionName.dll에 저장된 파일을 컴파일합니다.  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll /r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 다음 코드 예에서는 확장명 .vb인 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 파일에 대해 사용되는 명령을 보여 줍니다.  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll /r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]를 사용하여 데이터 처리 확장 프로그램을 디자인, 개발 및 빌드할 수도 있습니다. [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]에서 어셈블리를 개발하는 방법은 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 설명서를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
