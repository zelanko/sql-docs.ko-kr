---
title: 지원되는 SharePoint와 Reporting Services 서버의 조합 | Microsoft Docs
description: SharePoint 모드로 설치된 SQL Server Reporting Services 보고서 서버에는 SharePoint 서버에 설치하는 SharePoint의 버전과 SharePoint용 SQL Server Reporting Services 추가 기능(rsSharePoint.msi) 제품이 필요합니다.
ms.date: 12/04/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.custom: seo-lt-2019, seo-mmd-2019
ms.topic: conceptual
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
- rsSharePoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 56da894b141733357ff33ec820073c52836e4cca
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74866066"
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server"></a>지원되는 SharePoint와 Reporting Services 서버의 조합

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SharePoint 모드로 설치된 SQL Server Reporting Services 보고서 서버에는 SharePoint 서버에 설치하는 SharePoint의 버전과 SharePoint용 SQL Server Reporting Services 추가 기능(rsSharePoint.msi) 제품이 필요합니다. 이 항목에는 지원되는 조합이 요약되어 있습니다.

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>지원되는 SharePoint와 Reporting Services 구성 요소의 조합

 다음 표에서는 보고서 서버, SharePoint 제품용 Reporting Services 추가 기능, SharePoint 제품에 대해 지원되는 조합 형태를 요약해서 보여 줍니다. 다음 표에 나열되지 않은 조합은 지원되지 않습니다.

### <a name="supported-combinations"></a>지원되는 조합

||보고서 서버|추가 기능|SharePoint 버전|
|-|-------------------|-------------|------------------------|
|1|SQL Server 2016|SQL Server 2016|SharePoint 2016|
|2|SQL Server 2016|SQL Server 2016|SharePoint 2013|
|3|SQL Server 2014|SQL Server 2014|SharePoint 2013|
|4|SQL Server 2014|SQL Server 2014|SharePoint 2010|
|5|SQL Server 2012 SP4|SQL Server 2014 및 SQL Server 2012 SP4|SharePoint 2013|
|6|SQL Server 2012 SP3|SQL Server 2014 및 SQL Server 2012 SP3|SharePoint 2013|
|7|SQL Server 2012 SP2|SQL Server 2014 및 SQL Server 2012 SP2|SharePoint 2013|
|8|SQL Server 2012 SP1|SQL Server 2014 및 SQL Server 2012 SP1|SharePoint 2013|
|9|SQL Server 2012 및 SQL Server 2012 SP1*|SQL Server 2014|SharePoint 2010|
|10|SQL Server 2012|SQL Server 2012|SharePoint 2010|
|11|SQL Server 2008 R2|SQL Server 2014|SharePoint 2010|
|12|SQL Server 2008 R2|SQL Server 2012 및 SQL Server 2012 SP1 이상|SharePoint 2010|
|13|SQL Server 2008 R2|SQL Server 2008 R2|SharePoint 2010|
|14|SQL Server 2008 R2|SQL Server 2008 SP2|SharePoint 2007|
|15|SQL Server 2008 SP2|SQL Server 2008 R2|SharePoint 2010|
|16|SQL Server 2008 SP2|SQL Server 2008 및 SQL Server 2008 SP2|SharePoint 2007|

 *예외: 파워 뷰 통합은 지원되지 않습니다.

 추가 기능 다운로드 페이지에 대한 자세한 내용은 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)를 참조하세요.  

 **추가 고려 사항:**

- 팜 내의 모든 SharePoint 서버를 업그레이드해야 합니다. 여기에는 앱 및 웹 프런트 엔드 서버가 포함됩니다.

- Power View 통합을 비롯한 SharePoint 2016 지원에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 SQL Server 2016 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 버전이 필요합니다.

- Power View 통합을 비롯한 SharePoint 2013 지원에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 SQL Server 2012 SP1 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 버전이 필요합니다.

- 파워 뷰는 SQL Server 2012에서 도입되었습니다. 따라서 SharePoint 2010과의 파워 뷰 통합에는 SQL Server 2012 이상의 추가 기능이 필요합니다.

- SQL Server 2008 R2 추가 기능은 SQL Server 2012 이상의 보고서 서버에서 지원되지 않습니다. SharePoint 2010 필수 구성 요소 설치 관리자는 SQL Server 2008 R2 추가 기능을 자동으로 설치합니다. 이 추가 기능은 최신 버전의 추가 기능을 설치하기 전에 제거해야 합니다. 추가 기능의 내부 업그레이드는 지원되지 않습니다.

- **업그레이드:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능이 설치된 SharePoint 2010은 SharePoint 2013으로 해당 위치에서 업그레이드할 수 없습니다. SharePoint 2013에는 SQL Server 2012 SP1 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능 및 보고서 서버가 필요합니다. 업그레이드에 대한 자세한 내용은 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)을 참조하십시오.

## <a name="next-steps"></a>다음 단계

 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-components-of-sql-server-2017.md)   
 [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
