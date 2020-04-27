---
title: Integration Services 서비스에 대 한 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- viewing packages while running
- displaying packacges while running
- security [Integration Services], running packages
- packages [Integration Services], security
- current packages running
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 1088aafc-14c5-4e7d-9930-606a24c3049b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e3654be0afe51be6566a09897a2656dd53c77696
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062241"
---
# <a name="access-to-the-integration-services-service"></a>Integration Services 서비스 액세스
  패키지 보호 수준으로 패키지를 편집 및 실행할 수 있는 사용자를 제한할 수 있지만, 현재 서버에서 실행 중인 패키지 목록을 볼 수 있는 사용자 및 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 현재 실행 중인 패키지를 중지할 수 있는 사용자를 제한하려면 보다 높은 수준의 보호가 필요합니다.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스를 사용하여 실행 중인 패키지를 나열합니다. Windows Administrators 그룹의 멤버는 현재 실행 중인 모든 패키지를 보고 중지할 수 있습니다. Administrators 그룹의 멤버가 아닌 사용자는 자신이 시작한 패키지만 보고 중지할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스, 특히 원격 폴더를 열거할 수 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스를 실행하는 컴퓨터에 대한 액세스를 제한하는 것이 중요합니다. 허가 받은 사용자는 패키지의 열거를 요청할 수 있습니다. 서비스에서 패키지를 찾지 못하더라도 서비스는 폴더를 열거합니다. 이 폴더 이름은 악의적인 사용자에 의해 악용될 수 있습니다. 관리자가 원격 컴퓨터에서 폴더를 열거하도록 서비스를 구성한 경우 사용자는 일반적으로 볼 수 없는 폴더 이름도 볼 수 있습니다.  
  
  
