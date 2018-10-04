---
title: PowerPivot 데이터 새로 고침 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: ac8358a3-ee71-44c7-8ee6-ac7afe3ebaa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a3b87563bc8fc7908da703f6ff71165b61142738
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48221393"
---
# <a name="powerpivot-data-refresh"></a>PowerPivot 데이터 새로 고침
  PowerPivot 데이터가 포함된 통합 문서를 만든 후 통합 문서를 만들기 위해 원래 사용했던 원본의 업데이트된 정보를 가져오기 위해 쿼리나 명령을 다시 실행하여 정기적으로 데이터를 새로 고칠 수 있습니다. 이 프로세스를 `data refresh`라고 하며, [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]에서 요청 시 또는 SharePoint 팜의 응용 프로그램 서버에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로세스로 실행되는 예약된 작업으로 데이터를 새로 고칠 수 있습니다. 참조 항목:  
  
-   [SharePoint 2010에서 PowerPivot 데이터 새로 고침](../powerpivot-data-refresh-with-sharepoint-2010.md)  
  
-   [구성 PowerPivot 무인된 데이터 새로 고침 계정 &#40;SharePoint 용 PowerPivot&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)  
  
-   [PowerPivot 데이터 새로 고침에 대 한 저장 된 자격 증명 구성 &#40;SharePoint 용 PowerPivot&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
-   [데이터 새로 고침 예약 &#40;SharePoint 용 PowerPivot&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)  
  
-   [데이터 새로 고침 기록 보기 &#40;SharePoint 용 PowerPivot&#41;](view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 SharePoint Server 2013 Excel Services에서는 PowerPivot 데이터 모델의 데이터 새로 고침에 다른 아키텍처를 사용합니다. SharePoint 2013 지원 아키텍처는 Excel Services를 기본 구성 요소로 사용하여 PowerPivot 데이터 모델을 로드합니다. 이전에 사용한 데이터 새로 고침 아키텍처는 PowerPivot 시스템 서비스와 SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 사용하여 데이터 모델을 로드했습니다. 자세한 내용은 다음 항목을 참조하세요.  
>   
>  -   [SharePoint 2013에서 PowerPivot 데이터 새로 고침](power-pivot-data-refresh-with-sharepoint-2013.md)  
> -   [예약 된 데이터 새로 고침 및 통합 문서 업그레이드 &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
