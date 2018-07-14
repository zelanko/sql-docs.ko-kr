---
title: 데이터를 지원 하도록 ADO.NET Data Services 설치 피드 SharePoint 목록의 내보내기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f32527ae-f623-4e08-adfb-6d3262f5c2ac
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 888e3bcf01f3cbb33ae11a3961a6d492040afb1f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187730"
---
# <a name="install-adonet-data-services-to-support-data-feed-exports-of-sharepoint-lists"></a>ADO.NET Data Services를 설치하여 SharePoint 목록의 데이터 피드 내보내기 지원
  SharePoint 목록의 데이터 피드 내보내기를 수행하려면 ADO.NET Data Services가 필요합니다. 이 구성 요소는 SharePoint 2010의 SharePoint 필수 구성 요소 설치 관리자 프로그램에 포함되어 있지 않으므로 수동으로 설치해야 합니다.  
  
 이 필수 구성 요소가 없는 경우 데이터 피드로 내보내진 SharePoint 목록을 사용하려고 시도하면 다음 오류가 표시됩니다. "보안상의 이유로 이 XML 문서에는 DTD가 허용되지 않습니다. DTD 처리를 활성화하려면 XmlReaderSettings의 ProhibitDtd 속성을 false로 설정하고 이 설정을 XmlReader.Create 메서드로 전달합니다."  
  
 다음 지침에 따라 목록을 데이터 피드로 내보내도록 허용할 모든 SharePoint 서버에 ADO.NET Data Services를 설치합니다.  
  
### <a name="download-and-install-adonet-data-services"></a>ADO.NET Data Services 다운로드 및 설치  
  
1.  SharePoint 2010의 하드웨어 및 소프트웨어 요구 사항 설명서를 보려면 [하드웨어 및 소프트웨어 요구 사항(SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=169734)으로 이동하십시오.  
  
2.  **적용 가능한 소프트웨어에 대한 액세스**에서 현재 사용 중인 운영 체제(Windows Server 2008 SP2 또는 Windows Server 2008 R2)에 맞는 ADO.NET Data Services 3.5의 링크를 찾습니다.  
  
3.  링크를 클릭하여 서비스를 설치하는 설치 프로그램을 실행합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
