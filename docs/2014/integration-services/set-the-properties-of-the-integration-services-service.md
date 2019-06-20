---
title: Integration Services 서비스의 속성 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- Integration Services service, properties
ms.assetid: 3a8ad546-0f58-4b31-ab56-58d6313b1098
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c40ec2d7da7dc8f46644632d29b6fb8d1101ff9b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055634"
---
# <a name="set-the-properties-of-the-integration-services-service"></a>Integration Services 서비스 속성 설정
    
> [!IMPORTANT]  
>  이 항목에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 관리하는 Windows 서비스인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 대해 설명합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]는 이전 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 버전과의 호환성을 위한 서비스를 지원합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]부터는 Integration Services 서버의 패키지와 같은 개체를 관리할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 패키지를 관리하고 모니터링합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 처음 설치하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스가 시작되고 서비스의 시작 유형이 자동으로 설정됩니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스가 설치된 후에는 SQL Server 구성 관리자나 서비스 MMC 스냅인을 사용하여 서비스의 속성을 설정할 수 있습니다.  
  
 서비스가 패키지를 저장하고 관리하는 위치 등 서비스의 다른 중요한 기능을 구성하려면 서비스의 구성 파일을 수정해야 합니다. 자세한 내용은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](service/integration-services-service-ssis-service.md)을 참조하세요.  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-sql-server-configuration-manager"></a>SQL Server 구성 관리자를 사용하여 Integration Services 서비스의 속성을 설정하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, **Microsoft SQL Server**, **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
2.  **SQL Server 구성 관리자** 스냅인의 서비스 목록에서 **SQL Server Integration Services** 를 찾아 **SQL Server Integration Services**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **SQL Server Integration Services 속성** 대화 상자에서 다음을 수행할 수 있습니다.  
  
    -   **로그온** 탭을 클릭하여 계정 이름과 같은 로그온 정보를 확인합니다.  
  
    -   **서비스** 탭을 클릭하여 호스트 컴퓨터 이름과 같은 서비스에 대한 정보를 확인하고 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스의 시작 모드를 지정합니다.  
  
        > [!NOTE]  
        >  **고급** 탭에는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 대한 정보가 들어 있지 않습니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  **파일** 메뉴에서 **끝내기** 를 클릭하여 **SQL Server 구성 관리자** 스냅인을 닫습니다.  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-services"></a>서비스를 사용하여 Integration Services 서비스의 속성을 설정하려면  
  
1.  클래식 보기를 사용할 경우에는 **제어판**에서 **관리 도구**를 클릭하고 종류별 보기를 사용할 경우에는 제어판에서 **성능 및 유지 관리** 를 클릭한 후 **관리 도구**를 클릭합니다.  
  
2.  **서비스**를 클릭합니다.  
  
3.  **서비스** 스냅인에서 서비스 목록의 **SQL Server Integration Services** 를 찾은 다음 **SQL Server Integration Services**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
4.  **SQL Server Integration Services 속성** 대화 상자에서 다음을 수행할 수 있습니다.  
  
    -   **일반** 탭을 클릭합니다. 서비스를 사용하려면 시작 유형에 수동 또는 자동을 선택합니다. 서비스를 사용하지 않으려면 **시작 유형** 상자에서 사용 안 함을 선택합니다. 사용 안 함을 선택해도 현재 실행 중인 서비스가 중지되지는 않습니다.  
  
         서비스를 이미 사용하고 있는 경우 **중지** 를 클릭하여 서비스를 중지하거나 **시작** 을 클릭하여 서비스를 시작합니다.  
  
    -   **로그온** 탭을 클릭하여 로그온 정보를 보거나 편집합니다.  
  
    -   **복구** 탭을 클릭하여 서비스 실패 시 기본 컴퓨터의 응답을 봅니다. 사용자 환경에 맞게 이러한 옵션을 수정할 수 있습니다.  
  
    -   **종속성** 탭을 클릭하여 종속 서비스 목록을 봅니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에는 종속성이 없습니다.  
  
5.  **확인**을 클릭합니다.  
  
6.  시작 유형이 수동이거나 자동인 경우 필요에 따라 **SQL Server Integration Services** 를 마우스 오른쪽 단추로 클릭하고 **시작, 중지 또는 다시 시작**을 클릭합니다.  
  
7.  **파일** 메뉴에서 **끝내기** 를 클릭하여 **서비스** 스냅인을 닫습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 서비스 관리](../../2014/integration-services/manage-the-integration-services-service.md)  
  
  
