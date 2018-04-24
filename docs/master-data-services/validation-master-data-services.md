---
title: 유효성 검사(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98eb49e7-b190-4a21-8316-08c07cde14ed
caps.latest.revision: 12
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51cd2182820113030bdeb060ddc17997d93c2fda
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="validation-master-data-services"></a>유효성 검사(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 데이터의 유효성을 검사하여 정확성을 확인합니다. 일부 유효성 검사는 자동으로 발생하고, 일부 유효성 검사는 관리자가 만든 비즈니스 규칙을 기반으로 합니다.  
  
## <a name="when-data-validation-occurs"></a>데이터 유효성 검사가 수행되는 경우  
 유효성 검사는 서로 다른 시기에 발생하며 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 응용 프로그램에 다르게 표시됩니다.  
  
|유효성 검사 유형|표준 결정자|발생 시기|MasterData 관리자 웹 UI에 표시|Excel용 추가 기능에 표시|MDS 저장소에 데이터 저장 여부|  
|---------------------|-----------------------------|--------------------|---------------------------------------------------|-------------------------------------------|------------------------------------------|  
|비즈니스 규칙 유효성 검사|MDS 관리자|사용자가 데이터를 추가하거나 편집할 때 자동으로<br /><br /> 사용자가 비즈니스 규칙을 적용할 때 수동으로<br /><br /> 관리자가 **웹 응용 프로그램의** 버전 관리 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 기능 영역에서 비즈니스 규칙에 대해 버전의 유효성을 검사할 때 수동으로|유효성 검사 오류|ValidationStatus|예|  
|데이터 형식 및 내용 유효성 검사|MDS 관리자(특성의 길이 또는 데이터 형식과 같은 모델 개체를 만들 때)|사용자가 데이터를 추가하거나 편집할 때 자동으로|입력 오류|InputStatus|아니오|  
|데이터 형식 및 내용 유효성 검사|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|사용자가 데이터를 추가하거나 편집할 때 자동으로|입력 오류|InputStatus|아니오|  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|비즈니스 규칙을 만들고 이 규칙에 대해 데이터 유효성 검사를 수행하도록 규칙을 게시합니다.|[비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|비즈니스 규칙에 대해 데이터 버전의 유효성을 검사합니다. 관리자 전용입니다.|[비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)|  
|비즈니스 규칙에 대해 특정 하위 집합 데이터의 유효성을 검사합니다. **탐색기** 기능 영역에 대한 사용 권한을 가진 모든 사용자용입니다.|[비즈니스 규칙에 대해 특정 멤버 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|비즈니스 규칙에 대해 특정 하위 집합 데이터의 유효성을 검사합니다. **탐색기** 기능 영역에 대한 사용 권한을 갖고 있으며 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]을 사용하는 모든 사용자용입니다.|[비즈니스 규칙 적용&#40;Excel용 MDS 추가 기능&#41;](../master-data-services/microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)|  
  
## <a name="see-also"></a>참고 항목  
 [비즈니스 규칙&#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
