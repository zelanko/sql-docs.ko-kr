---
title: PowerPivot을 배포 하 고 Power View-다층 계층 SharePoint 2016 팜에서 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c014d51f6f19efae02b07c9b6ea20ebd2ae7265a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-powerpivot-and-power-view---multi-tier-sharepoint-2016-farm"></a>PowerPivot을 배포 하 고 Power View-다층 계층 SharePoint 2016 팜에서
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  **요약:** 이 백서에서는 SharePoint Server 2016, Office Online Server 및 SharePoint 2016용 SQL Server 2016 BI 스택의 Preview 릴리스를 기준으로 하여 서버가 여러 대 포함되어 있는 SharePoint 팜에서 Microsoft BI 데모 환경을 배포하고 구성하는 자세한 단계별 지침을 SharePoint 관리자와 설계자에게 제공합니다. 여기서는 먼저 중요한 아키텍처 변경 내용과 해당하는 시스템 종속성을 간략하게 소개한 다음, 소프트웨어 및 구성 요구 사항과 3가지 주요 단계를 통해 BI 기능을 사용하도록 설정하고 확인하기 위한 권장 배포 경로를 대략적으로 설명합니다. 또한 이 백서에서는 SharePoint Server 2016 베타 2, Office Online Server Preview 및 SQL Server 2016 CTP 3.1 릴리스의 알려진 문제에 대해 설명하고 적합한 해결 방법을 제안합니다. 최종 제품 버전에서는 이러한 해결 방법을 더 이상 사용할 필요가 없습니다. RTM 릴리스를 배포할 때는 이 백서의 업데이트된 버전을 확인하세요.  
  
 **작성자:** Kay Unkroth, Jason Haak  
  
 **기술 검토자:** Adam Saxton, Anne Zorner, Craig Guyer, Frank Weigel, Gregory Appel, Heidi Steen, Kasper de Jonge, Kirk Stark, Klaus Sobel, Mike Plumley, Mike Taghizadeh, Patrick Wheeler, Riccardo Muti, Steve Hord  
  
 **게시일:** 2016년 1월  
  
 **적용 대상:** SQL Server 2016 CTP3.1, SharePoint 2016 Preview, Office Online Server Preview  
  
 문서를 검토하려면 [다층 계층 SharePoint 2016 팜에서 SQL Server 2016 파워 피벗 및 파워 뷰 배포](http://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Deploying%20SQL%20Server%202016%20PowerPivot%20and%20Power%20View%20in%20a%20Multi-Tier%20SharePoint%202016%20Farm.docx) Word 문서를 다운로드하세요.  
  
  
