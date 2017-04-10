---
title: "새 사용자 역할(Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.reportserver.newrole.f1"
ms.assetid: 9f76a235-0b58-479c-8e5b-50588091b71c
caps.latest.revision: 26
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 26
---
# 새 사용자 역할(Management Studio)
  이 페이지를 사용하여 항목 수준의 역할 정의를 만들 수 있습니다. 항목 수준의 역할 정의란 폴더, 보고서, 모델, 리소스 및 공유 데이터 원본과 관련하여 사용자가 수행할 수 있는 태스크를 열거하는 작업의 명명된 모음입니다. 항목 수준의 역할 정의의 예로 보고서 최종 사용자가 폴더를 이동하고 보고서를 보는 데 필요한 동작 종류를 식별하는 미리 정의된 브라우저 역할을 들 수 있습니다.  
  
 역할 정의 개수는 적은 것이 좋습니다. 대부분의 조직에는 서너 개의 역할 정의만 있으면 충분합니다. 그러나 미리 정의된 역할 정의가 불충분할 경우 수정하거나 새로 만들 수 있습니다.  
  
> [!NOTE]  
>  역할 정의는 기본 모드로 실행되는 보고서 서버에만 사용되며 보고서 서버가 SharePoint 통합 모드로 구성된 경우 이 페이지를 사용할 수 없습니다.  
  
## 옵션  
 **이름**  
 역할 정의의 이름을 입력합니다. 역할 정의 이름은 보고서 서버 네임스페이스 내에서 고유해야 합니다. 이름은 하나 이상의 영숫자 문자를 포함해야 합니다. 공백과 특정 기호도 포함할 수 있습니다. 이름 지정 시에는 다음 문자를 사용하지 마십시오.  
  
 ; ? : @ & = + , $ / * \< >  
  
 " /  
  
 **Description**  
 역할 사용 방법을 설명하고 역할에서 지원하는 작업을 나열하는 설명을 입력합니다.  
  
 **태스크**  
 이 역할을 통해 수행할 수 있는 태스크를 선택합니다. 새 태스크를 만들거나 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 지원하는 기존 작업을 수정할 수 없습니다. 항목 수준의 역할 정의에서는 항목 수준의 태스크만 사용할 수 있습니다.  
  
 **태스크 설명**  
 작업에서 지원하는 작업 또는 사용 권한을 열거하는 태스크에 대한 설명을 표시합니다.  
  
## 관련 항목:  
 [Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [역할 정의](../../reporting-services/security/role-definitions.md)  
  
  