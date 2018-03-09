---
title: "보안 폴더 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- high-security folders [Reporting Services]
- low-security folders
- folders [Reporting Services], security
- security [Reporting Services], folders
ms.assetid: 0fd91f77-0143-476b-9af0-87293be78e44
caps.latest.revision: "34"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e7d20035ce370e8e096963afe20083a82eed19a2
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="secure-folders"></a>보안 폴더
  폴더 보안 설정은 보고서 서버의 모든 내용에 보안을 설정하기 위한 기본 토대입니다. 보안 설정은 폴더 구조를 통해 상속되므로 폴더 계층의 큰 부분이나 작은 부분을 지정하여 특정 종류의 액세스를 허용할 수 있습니다.  
  
 보안 설정이 높은 폴더는 기밀 보고서를 저장하거나 준비 영역으로 사용할 수 있습니다. 예를 들어 보고서를 최종 위치로 이동하기 전에 보고서 테스트용으로 폴더를 사용할 수 있습니다. 이 영역에 대한 액세스를 제어하려면 보고서 작성자만 항목을 추가하고 삭제할 수 있도록 하는 하나의 역할 할당과 테스터가 보고서 실행은 할 수 있지만 항목을 추가하거나 제거할 수 없도록 하는 또 다른 역할 할당을 정의할 수 있습니다. 역할 할당이 테스터 및 보고서 작성자에 대해 명시적으로 정의되므로 로컬 시스템 관리자를 제외한 다른 사용자는 폴더에 액세스할 수 없습니다.  
  
 보안 설정이 낮은 폴더는 쉽게 액세스할 수 있는 보고서를 저장하는 데 사용할 수 있습니다.  
  
 폴더 보안 설정은 보고서 서버 폴더 계층의 루트 노드인 홈 폴더에서 시작하는 항목 수준의 보안의 기본을 이룹니다. 보안 설정은 상속되므로 홈 폴더에 대해 적정 수준으로 제한된 보안 정책을 설정하는 게 좋습니다. 홈 폴더 역할 할당에 **브라우저** 역할을 사용하면 보기 전용 액세스를 제공하여 보안 정책이 적절히 제한됩니다.  
  
## <a name="tasks-and-folder-access"></a>태스크 및 폴더 액세스  
 폴더에 대한 역할 할당을 만들 때는 다음 표에 나열된 태스크를 고려하십시오.  
  
|태스크 선택|제공되는 사용 권한|  
|----------------------|---------------------------|  
|폴더 보기|폴더 계층과 폴더가 생성 및 수정된 시기를 나타내는 읽기 전용 속성을 봅니다.<br /><br /> 사용자가 "보고서 보기", "모델 보기", "리소스 보기" 및 "데이터 원본 보기"가 포함되는 역할에 할당되지 않으면 폴더의 항목을 볼 수 없습니다.|  
|폴더 관리|폴더 속성을 보거나, 이름 또는 설명을 변경하거나, 폴더를 다른 위치로 이동합니다. 이 태스크를 지정하면 사용자가 폴더를 만들 수 있습니다.|  
|보고서 관리|파일 시스템의 보고서를 폴더에 추가하고, 보고서 디자이너의 보고서를 보고서 서버에 게시합니다.|  
|데이터 원본 관리|폴더에 새 공유 데이터 원본 항목을 추가하거나 기존 공유 데이터 원본을 변경합니다.|  
|항목의 보안 설정|폴더에 대한 액세스를 제어하는 역할 할당을 생성 및 수정합니다. 이 태스크는 "폴더 보기"나 "폴더 관리"와 함께 사용해야 합니다. 그렇지 않으면 사용자가 항목을 선택할 수 없게 되므로 효과가 없습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [보고서 및 리소스 보안](../../reporting-services/security/secure-reports-and-resources.md)   
 [공유 데이터 원본 항목 보안](../../reporting-services/security/secure-shared-data-source-items.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
