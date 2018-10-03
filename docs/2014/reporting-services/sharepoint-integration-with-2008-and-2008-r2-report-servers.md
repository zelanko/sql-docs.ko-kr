---
title: SharePoint 통합 2008 및 2008 R2 보고서 서버 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d9f51c37-b071-45d0-baec-f82fa6db366f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 13d4141b25a194a3d2536e2ebf3246eefe659f3f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112771"
---
# <a name="sharepoint-integration-with-2008-and-2008-r2--report-servers"></a>2008 및 2008 R2 보고서 서버와 SharePoint 통합
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 릴리스에서는 SharePoint 모드가 SharePoint 공유 서비스를 기반으로 하는 아키텍처를 도입했습니다. 새 기능에 대한 관리는 **서비스 관리** 및 **관리자 서비스 응용 프로그램** 페이지의 SharePoint 중앙 관리에서 완료됩니다. SharePoint 통합에 대한 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 이전 아키텍처는 SharePoint 2010 제품의 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 추가 기능에서도 지원되므로 SharePoint 2010을 이전 버전의 보고서 서버와 통합할 수 있습니다.  
  
 이전 아키텍처를 관리하는 데 사용되는 SharePoint 중앙 관리 페이지는 다음 위치에 있습니다.  
  
1.  SharePoint 중앙 관리에서 **일반 응용 프로그램 설정**을 클릭합니다.  
  
2.  **SQL Server Reporting Services(2008 및 2008 R2)** 그룹에는 이전 아키텍처에 대한 링크와 관리 페이지가 포함되어 있습니다.  
  
## <a name="server-integration-architecture"></a>서버 통합 아키텍처  
 보고서 서버를 SharePoint 제품 인스턴스와 통합하면 항목과 속성이 SharePoint 콘텐츠 데이터베이스에 저장됩니다. 이로 인해 콘텐츠가 저장, 보안 유지 및 액세스되는 방법에 영향을 주는 서버 기술이 더욱 폭넓게 통합됩니다.  
  
 보고서 항목과 속성을 SharePoint 콘텐츠 데이터베이스에 저장하면 SharePoint 라이브러리에서 보고서 서버 콘텐츠 형식을 찾아보고, SharePoint 사이트에 호스팅되는 기타 비즈니스 문서에 대한 액세스를 제어하는 동일한 사용 권한 수준 및 인증 공급자를 사용하여 항목의 보안을 유지하고, 공동 작업 및 문서 관리 기능을 사용하여 수정할 보고서를 체크 인 및 체크 아웃하고, 경고를 사용하여 항목의 변경 여부를 파악하고, 응용 프로그램 내의 페이지와 사이트에서 보고서 뷰어 웹 파트를 포함하거나 사용자 지정할 수 있습니다. SharePoint 사이트 내에서 권한이 충분한 경우 공유 데이터 원본에서 보고서 모델을 생성하고 보고서 작성기를 사용하여 보고서를 만들 수도 있습니다.  
  
 보고서 서버는 계속해서 모든 데이터 처리, 렌더링 및 배달을 제공합니다. 또한 스냅숏 및 보고서 기록에 대해 모든 예약된 보고서 처리를 지원합니다. SharePoint 사이트에서 보고서를 열면 Report Server 엔드포인트가 보고서 서버에 연결되고, 세션을 만들고, 처리할 보고서를 준비하고, 데이터를 검색하고, 보고서를 보고서 레이아웃으로 병합하고, 이를 보고서 뷰어 웹 파트에 표시합니다. 보고서가 열려 있는 동안 보고서를 다른 응용 프로그램 형식으로 내보내거나, 기본 숫자로 드릴하거나 관련 보고서를 클릭 방문하여 데이터와 상호 작용할 수 있습니다. 내보내기 및 보고서 상호 작용 작업은 보고서 서버에서 수행됩니다.  
  
 보고서 서버는 작업 및 데이터를 SharePoint와 동기화하고, 처리하는 파일에 대한 정보를 추적합니다. 보고서 서버 항목의 속성이나 설정을 수정하는 경우 변경 내용은 SharePoint 데이터베이스에 저장된 다음 보고서 서버에 내부 저장소를 제공하는 보고서 서버 데이터베이스에 복사됩니다.  
  
## <a name="related-content"></a>관련 내용  
 [SharePoint에서 보고서 서버 및 파워 뷰 통합 사이트 모음 기능 활성화](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)  
 이전 릴리스의 보고서 서버와의 통합에 필요한 보고서 서버 기능을 활성화하는 방법에 대해 설명합니다.  
  
  
