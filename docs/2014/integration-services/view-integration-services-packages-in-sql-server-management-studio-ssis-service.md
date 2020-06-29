---
title: SQL Server Management Studio에서 Integration Services 패키지 보기 (SSIS 서비스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- viewing packages
- connections [Integration Services], packages
ms.assetid: 783e653c-0f1f-45ed-b3ef-5ba07b019f27
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 190ba24d6f13d51233e21f8a829e3ce05d31b4b3
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85420160"
---
# <a name="view-integration-services-packages-in-sql-server-management-studio-ssis-service"></a>SQL Server Management Studio에서 Integration Services 패키지 보기(SSIS 서비스)
    
> [!IMPORTANT]  
>  이 항목에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 관리하는 Windows 서비스인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 대해 설명합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 는 이전 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]버전과의 호환성을 위한 서비스를 지원합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]부터는 Integration Services 서버의 패키지와 같은 개체를 관리할 수 있습니다.  
  
 이 절차에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에 연결하고 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에서 관리하는 패키지 목록을 보는 방법을 설명합니다.  
  
### <a name="to-connect-to-integration-services"></a>Integration Services에 연결하려면  
  
1.  **시작**을 클릭하고 **모든 프로그램**, **Microsoft SQL Server**를 차례로 가리킨 다음 **SQL Server Management Studio**를 클릭합니다.  
  
2.  **서버에 연결** 대화 상자의 **서버 유형** 목록에서 **Integration Services** 를 선택하고 **서버 이름** 상자에 서버 이름을 지정한 다음 **연결**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에 연결할 수 없으면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스가 실행되고 있지 않는 것일 수 있습니다. 이 서비스의 상태를 확인하려면 **시작**을 클릭하고 **모든 프로그램**, **Microsoft SQL Server**, **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다. 왼쪽 창에서 **SQL Server 서비스**를 클릭하고 오른쪽 창에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스를 찾습니다. 서비스가 실행되지 않았으면 서비스를 시작합니다.  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 가 열립니다. 기본적으로 SQL Server Management Studio의 왼쪽 아래에는 개체 탐색기 창이 열립니다. 개체 탐색기가 열려 있지 않으면 **보기** 메뉴에서 **개체 탐색기** 를 클릭합니다.  
  
### <a name="to-view-the-packages-that-integration-services-service-manages"></a>Integration Services 서비스에서 관리하는 패키지를 보려면  
  
1.  개체 탐색기에서 저장된 패키지 폴더를 확장합니다.  
  
2.  저장된 패키지 하위 폴더를 확장하여 패키지를 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SSIS 서비스를 &#40;패키지 관리&#41;](service/package-management-ssis-service.md)   
 [SQL Server Management Studio 사용](../database-engine/use-sql-server-management-studio.md)  
  
  
