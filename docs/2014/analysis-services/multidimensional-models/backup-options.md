---
title: 백업 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [Analysis Services]
- databases [Analysis Services], backing up
ms.assetid: 02d33fc9-f3f4-4b85-8b90-449b68625cf7
author: minewiskan
ms.author: owend
ms.openlocfilehash: f9fc674e699a3078ebd39d50fde96d632ae20493
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544635"
---
# <a name="backup-options"></a>백업 옵션
  여러 가지 방법으로 데이터베이스를 백업할 수 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 있으며, 모두 서버 관리자와 데이터베이스 관리자 권한이 필요 합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **백업** 대화 상자를 열고 적절한 옵션 구성을 선택한 후 백업을 실행할 수 있습니다. 또는 파일에 이미 지정된 설정을 사용하는 스크립트를 만들어 저장하고 필요할 때마다 스크립트를 실행할 수 있습니다.  
  
## <a name="backup-and-synchronize"></a>백업 및 동기화  
 데이터베이스가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]원격 인스턴스에 있는 경우 동기화 기능을 사용하여 데이터베이스를 로컬 인스턴스로 백업할 수 있습니다. 이 방법으로 데이터베이스의 개발 빌드를 프로덕션으로 이동할 수 있습니다. 기존의 파일 기반 백업과 복원을 사용하여 개발 빌드를 프로덕션으로 이동할 수도 있으나 동기화를 사용하면 추가 기능을 이용할 수 있습니다. 예를 들어 개발 컴퓨터와 프로덕션 컴퓨터의 보안 설정이 다른 경우 동기화를 사용하면 해당 설정을 유지하고 역할을 제외한 모든 개체를 동기화할 수 있습니다. 또한 동기화는 일반적으로 원본 컴퓨터와 대상 컴퓨터에서 다른 개체에 대해 증분 업데이트를 수행합니다. 백업/복원 기능으로는 이러한 증분 백업을 사용할 수 없습니다. 자세한 내용은 [Synchronize Analysis Services Databases](synchronize-analysis-services-databases.md)을(를) 참조하세요.  
  
> [!IMPORTANT]  
>  Analysis Services 서비스 계정에는 각 파일에 대해 지정한 백업 위치에 쓸 수 있는 권한이 있어야 합니다. 또한 사용자는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 관리자 역할이나 백업할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버를 가지고 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 백업 대화 상자 &#40;Analysis Services 다차원 데이터&#41;](../backup-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Analysis Services 데이터베이스 백업 및 복원](backup-and-restore-of-analysis-services-databases.md)   
 [Backup 요소 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [데이터베이스 백업, 복원 및 동기화&#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
