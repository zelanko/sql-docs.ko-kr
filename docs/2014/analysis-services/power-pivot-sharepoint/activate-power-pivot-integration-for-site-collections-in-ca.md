---
title: 중앙 관리에서 사이트 모음에 대해 PowerPivot 기능 통합 활성화 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 62a27e53-446a-42d7-b5db-c009e02d4904
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c5a8e3f2930d7975f8c75c8f89ab90b78461a650
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072004"
---
# <a name="activate-powerpivot-feature-integration-for-site-collections-in-central-administration"></a>중앙 관리에서 사이트 모음에 대해 PowerPivot 기능 통합 활성화
  기존 팜 설치 옵션을 사용하여 SQL Server SharePoint용 PowerPivot을 설치한 경우 특정 사이트 모음에 대해 PowerPivot 기능 통합을 활성화해야 합니다. 새 서버 옵션을 사용해 SharePoint용 PowerPivot을 설치한 경우에는 SQL Server 설치 프로그램에서 배포를 구성할 때 루트 사이트 모음에 대해 PowerPivot 기능 통합을 이미 활성화했기 때문에 이 태스크를 건너뛰어도 됩니다.  
  
 사이트 모음 수준에서 기능을 활성화하면 사이트에서 애플리케이션 페이지 및 템플릿을 사용할 수 있습니다. 여기에는 예약된 데이터 새로 고침을 구성하는 애플리케이션 페이지와 PowerPivot 갤러리 및 데이터 피드 라이브러리를 구성하는 애플리케이션 페이지가 포함됩니다.  
  
 PowerPivot 쿼리 처리를 지원하는 각 사이트 모음에 대해 PowerPivot 통합을 활성화해야 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 사이트 모음 관리자여야 합니다.  
  
## <a name="activate-powerpivot-features"></a>PowerPivot 기능 활성화  
  
1.  SharePoint 사이트에서 **사이트 작업**을 클릭합니다.  
  
     기본적으로 SharePoint 웹 애플리케이션은 포트 80을 통해 액세스됩니다. 즉, http://를 입력 하 여 SharePoint 사이트를 자주 액세스할 수는\<컴퓨터 이름 >를 루트 사이트 모음을 엽니다.  
  
2.  **사이트 설정**을 클릭합니다.  
  
3.  사이트 컬렉션 관리에서 **사이트 컬렉션 기능**을 클릭합니다.  
  
4.  페이지를 아래로 스크롤하여 **PowerPivot 통합 사이트 컬렉션 기능**을 찾습니다.  
  
5.  **활성화**를 클릭합니다.  
  
6.  각 사이트를 열고 **사이트 작업**을 클릭하여 추가 사이트 모음에 대해 위 단계를 반복합니다.  
  
## <a name="see-also"></a>관련 항목  
 [중앙 관리에서 PowerPivot 서버 관리 및 구성](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [초기 구성 &#40;SharePoint 용 PowerPivot&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [SharePoint 2010용 PowerPivot 설치](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
