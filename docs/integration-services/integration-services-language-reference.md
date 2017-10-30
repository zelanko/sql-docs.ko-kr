---
title: "Integration Services 언어 참조 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
ms.assetid: c67b72f1-0a1e-42f0-878a-84e85efc915b
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9fe4120f8a5dc93517e8eb35b13e7fe5252be6b6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-language-reference"></a>Integration Services 언어 참조
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 섹션에서는 [!INCLUDE[tsql](../includes/tsql-md.md)] 인스턴스에 배포된 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 관리하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] API에 대해 설명합니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]는 개체, 설정 및 작업 데이터를 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그라는 데이터베이스에 저장합니다. 기본 이름은 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] SSISDB 카탈로그가 합니다. 카탈로그에 저장되는 개체에는 프로젝트, 패키지, 매개 변수, 환경 및 작업 기록이 있습니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그는 사용자에게 표시되지 않는 내부 테이블에 해당 데이터를 저장합니다. 그러나 공용 뷰 집합 쿼리를 통해 이 데이터베이스에서 필요한 정보를 얻을 수 있습니다. 또한 카탈로그는 카탈로그에 대한 일반 태스크를 수행하는 데 사용할 수 있는 저장 프로시저 집합을 제공합니다.  
  
 일반적으로 카탈로그의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 열어서 관리합니다. 그러나 데이터베이스 뷰 및 저장 프로시저를 직접 사용하거나 관리되는 API를 호출하는 사용자 지정 코드를 작성할 수도 있습니다. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 및 관리되는 API는 뷰를 쿼리하고 이 섹션에 설명된 저장 프로시저를 호출하여 많은 태스크를 수행합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [뷰 &#40; Integration Services 카탈로그 &#41;](../integration-services/system-views/views-integration-services-catalog.md)  
 뷰를 쿼리하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체, 설정 및 작업 데이터를 검사합니다.  
  
 [저장 프로시저 &#40; Integration Services 카탈로그 &#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
 저장 프로시저를 호출하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체 및 설정을 추가, 제거 또는 수정합니다.  
  
 [함수&#40;Integration Services 카탈로그&#41;](http://msdn.microsoft.com/library/9f2aec85-3d4c-415f-b1f8-8328a60b1c7f)  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 관리하는 함수를 호출합니다.  
  
  

