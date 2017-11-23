---
title: "SQL Server 2016 PowerPivot 및 SharePoint 2016의 파워 뷰 배포 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2d0a9834-db91-403f-847c-79a8f49fc916
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d688ba6f378ca6ce4cebab95ce67572b33f27068
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="deploying-sql-server-2016-powerpivot-and-power-view-in-sharepoint-2016"></a>SharePoint 2016에서 SQL Server 2016 PowerPivot 및 파워 뷰 배포
  **요약:** 이 백서에서는 SharePoint Server 2016, Office Online Server 및 SharePoint 2016용 SQL Server 2016 BI 스택의 Preview 릴리스를 기준으로 하여 Microsoft BI 데모 환경을 배포하고 구성하는 자세한 단계별 지침을 SharePoint 관리자와 설계자에게 제공합니다. 여기서는 먼저 중요한 아키텍처 변경 내용과 해당하는 시스템 종속성을 간략하게 소개한 다음, 소프트웨어 및 구성 요구 사항과 3가지 주요 단계를 통해 BI 기능을 사용하도록 설정하고 확인하기 위한 권장 배포 경로를 대략적으로 설명합니다. 또한 이 백서에서는 SharePoint Server 2016 베타 2, Office Online Server Preview 및 SQL Server 2016 CTP 3.1 릴리스의 알려진 문제에 대해 설명하고 적합한 해결 방법을 제안합니다. 최종 제품 버전에서는 이러한 해결 방법을 더 이상 사용할 필요가 없습니다. RTM 릴리스를 배포할 때는 이 백서의 업데이트된 버전을 확인하세요.  
  
 **작성자:** Kay Unkroth  
  
 **기술 검토자:** Adam Saxton, Anne Zorner, Craig Guyer, Frank Weigel, Gregory Appel, Heidi Steen, Jason Haak, Kasper de Jonge, Kirk Stark, Klaus Sobel, Mike Plumley, Mike Taghizadeh, Patrick Wheeler, Riccardo Muti, Steve Hord  
  
 **게시일:** 2015년 12월  
  
 **적용 대상:** SQL Server 2016 CTP3.1, SharePoint 2016 Preview, Office Online Server Preview  
  
 문서를 검토하려면 [SharePoint 2016에서 SQL Server 2016 PowerPivot 및 파워 뷰 배포](http://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Deploying%20SQL%20Server%202016%20PowerPivot%20and%20Power%20View%20in%20SharePoint%202016.docx) Word 문서를 다운로드하세요.  
  
  
