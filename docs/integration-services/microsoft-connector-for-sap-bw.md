---
title: Microsoft Connector for SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5281f080-53d5-4679-aa26-f4cd4ac7a2df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4555f8ac86bb3755aa2357ced05dec5d54d038c6
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58272903"
---
# <a name="microsoft-connector-for-sap-bw"></a>Microsoft Connector for SAP BW
  [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW는 SAP Netweaver BW 버전 7 시스템에서 데이터를 추출하거나 해당 시스템으로 데이터를 로드하는 데 사용할 수 있는 3가지 구성 요소 집합으로 구성됩니다.  
  
 SQL Server 2016용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW는 SQL Server 2016 기능 팩의 구성 요소입니다. Connector for SAP BW 및 해당 설명서를 설치하려면 [SQL Server 2016 기능 팩 웹 페이지](https://go.microsoft.com/fwlink/?LinkId=746297)에서 설치 관리자를 다운로드하여 실행하세요.  

> [!IMPORTANT]
> Microsoft는 업데이트된 버전의 SAP BW용 커넥터를 제공하지 않습니다. Microsoft는 타사에서 개발된 SAP BW용 소스 코드 구성 요소를 소유하지 않으며 결과적으로 업데이트할 수 없습니다. [Theobald Software](https://theobald-software.com/en/xtract-is-productinfo.html) 등 Microsoft ISV 파트너로부터 최신 SAP 연결 구성 요소를 구매하는 것이 좋습니다. Microsoft의 ISV 파트너는 Azure에서 설치하기 위한 SSIS용 SAP 연결 구성 요소를 적용했습니다.
 
> [!IMPORTANT]  
>  Microsoft Connector for SAP BW 설명서에서는 사용자가 SAP Netweaver BW 환경에 대해 잘 알고 있다고 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP Netweaver BW에서 데이터를 추출하려면 추가 SAP 라이선스가 필요합니다. SAP에서 이러한 요구 사항을 확인하십시오.  
  
## <a name="components"></a>구성 요소  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW에는 다음 구성 요소가 포함되어 있습니다.  
  
-   **SAP BW 원본** - SAP BW 원본은 SAP Netweaver BW 버전 7 시스템에서 데이터를 추출할 수 있도록 지원하는 데이터 흐름 원본 구성 요소입니다.  
  
-   **SAP BW 대상** - SAP BW 대상은 SAP Netweaver BW 버전 7 시스템으로 데이터를 로드할 수 있도록 지원하는 데이터 흐름 대상 구성 요소입니다.  
  
-   **SAP BW 연결 관리자** - SAP BW 연결 관리자는 SAP BW 원본 또는 SAP BW 대상을 SAP Netweaver BW 버전 7 시스템으로 연결합니다.  
  
 SAP BW 연결 관리자, 원본 및 대상을 구성하고 사용하는 방법을 제시하는 연습은 [SAP BI 7.0에서 SQL Server Integration Services 사용](https://go.microsoft.com/fwlink/?LinkId=301897)백서를 참조하십시오. 또한 이 백서는 SAP BW에 필요한 개체를 구성하는 방법을 보여 줍니다.  
  
## <a name="documentation"></a>설명서  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW의 이 도움말 파일에는 다음 항목과 섹션이 포함되어 있습니다.  
  
 [Microsoft Connector for SAP BW 설치](../integration-services/installing-the-microsoft-connector-for-sap-bw.md)  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW의 설치 요구 사항에 대해 설명합니다.  
  
 [Microsoft Connector for SAP BW 구성 요소](../integration-services/microsoft-connector-for-sap-bw-components.md)  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW의 각 구성 요소에 대해 설명합니다.  
  
 [Microsoft Connector for SAP BW F1 도움말](../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW에 포함된 각 구성 요소의 사용자 인터페이스에 대해 설명합니다.  
  
  
