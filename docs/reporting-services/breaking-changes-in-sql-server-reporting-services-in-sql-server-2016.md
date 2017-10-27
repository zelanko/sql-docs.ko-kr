---
title: "SQL Server 2016에서 SQL Server Reporting Services의 주요 변경 내용 | Microsoft Docs"
ms.date: 07/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: 121
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 6348d05b8dbe6c8ab1a682388b4e69ce438e6a12
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---

# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2016"></a>SQL Server 2016에서 SQL Server Reporting Services의 주요 변경 내용

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

이 항목에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 주요 변경 내용에 대해 설명합니다. 이러한 변경 내용에 따라 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기반을 둔 응용 프로그램, 스크립트 또는 기능을 사용하지 못할 수도 있습니다. 이러한 문제는 업그레이드할 때나 사용자 지정 스크립트 또는 보고서에서 발생할 수 있습니다.

## <a name="security-extensions"></a>보안 확장 프로그램

새 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]에서 작동하도록 사용자 지정 보안 확장 프로그램을 약간 수정해야 합니다. 보안 확장 프로그램에서는 IAuthenticationExtension2 인터페이스를 사용해야 합니다.

## <a name="wmi-provider"></a>WMI 공급자

[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 응용 프로그램 이름이 "ReportManager"에서 "ReportServerWebApp"으로 변경됩니다.

## <a name="next-steps"></a>다음 단계

[SQL Server 2016에서 SQL Server Reporting Services의 동작 변경](../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)  
[Reporting Services (SSRS)의 새로운 기능](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)   
[SQL Server 2016에서 SQL Server Reporting Services에서 사용 되지 않는 기능](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)    
[SQL Server 2016의 SQL Server Reporting Services에서 중단된 기능](../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)

