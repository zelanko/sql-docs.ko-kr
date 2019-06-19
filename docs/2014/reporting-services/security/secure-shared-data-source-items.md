---
title: 공유 데이터 원본 항목 보안 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
- security [Reporting Services], data sources
ms.assetid: 7299e498-0a1a-4821-a22a-5199bb773ce0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2e3c7b1ec37eea31aef0d381815e4286f993c827
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101647"
---
# <a name="secure-shared-data-source-items"></a>공유 데이터 원본 항목 보안 설정
  공유 데이터 원본 항목에 대한 보안을 설정하여 해당 항목에 대한 액세스를 허용하거나 허용하지 않을 수 있습니다.  
  
 사용자가 보고서 자체를 볼 수 있도록 인증된 경우 공유 데이터 원본에 대해 최소 액세스 권한(예: **브라우저** 역할을 통해서 허용되는 액세스)이 있는 사용자는 해당 항목을 사용하는 보고서 목록을 볼 수 있습니다.  
  
 추가 액세스 권한(예: **내용 관리자** 역할을 통해서 허용되는 액세스)이 있는 사용자는 공유 데이터 원본에 대한 속성을 보거나 설정할 수 있습니다.  
  
 보안을 설정하려면 공유 데이터 원본에 대한 액세스 권한이 있는 사용자 또는 그룹 계정을 지정하는 역할 할당을 만듭니다. 공유 데이터 원본 항목에 대한 액세스 권한이 있는 사용자는 해당 항목의 이름, 설명, 연결 문자열 또는 자격 증명 정보를 변경할 수 있습니다.  
  
## <a name="tasks-and-access-to-items"></a>태스크 및 항목 액세스  
 역할 할당을 만들 때 이러한 태스크가 포함된 역할을 사용하여 사용자 및 그룹에 적절한 사용 권한을 할당할 수 있습니다.  
  
|태스크 선택|사용자에게 제공되는 사용 권한|  
|----------------------|---------------------------------|  
|데이터 원본 보기|폴더 계층에 있는 공유 데이터 원본 항목을 봅니다. 이 태스크가 없으면 항목이 사용자에게 표시되지 않으므로 데이터 원본이 사용 가능한지 여부를 알 수 없습니다.|  
|데이터 원본 관리|이름, 설명 및 연결 정보를 지정하는 속성을 봅니다. 이 태스크는 폴더 계층에 공유 데이터 원본 항목을 표시하는 데에도 사용됩니다. 이 태스크를 선택하면 "데이터 원본 보기" 작업을 생략할 수 있습니다.|  
|항목의 보안 설정|공유 데이터 원본에 대한 액세스를 제어하는 역할 할당을 만들고 수정합니다. 이 태스크는 "데이터 원본 보기" 또는 "데이터 원본 관리" 작업과 함께 사용해야 합니다. 그렇지 않으면 사용자가 항목을 선택할 수 없으므로 효과가 없습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [보고서 데이터 원본 관리](../report-data/manage-report-data-sources.md)   
 [보안 폴더](secure-folders.md)   
 [보고서 및 리소스 보안](secure-reports-and-resources.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](granting-permissions-on-a-native-mode-report-server.md)   
 [Reporting Services 데이터 원본에 자격 증명 저장](../report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
