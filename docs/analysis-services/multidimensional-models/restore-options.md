---
title: Analysis Services 복원 옵션 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9565c48186efc3fff43daa77cfc5e3525c3f5d37
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072560"
---
# <a name="restore-options"></a>복원 옵션
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스는 여러 가지 방법으로 복원할 수 있으며 어떤 방법에서든 서버 컴퓨터 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 관리자 권한이 필요합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 복원할 경우 **에서** 데이터베이스 복원 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자를 열고 적합한 옵션 구성을 선택한 다음 대화 상자에서 복원을 실행할 수 있습니다. 또는 파일에 이미 지정된 설정을 사용하는 스크립트를 만들어 저장하고 필요할 때마다 스크립트를 실행할 수 있습니다. 이 방식으로 다음 섹션에 설명된 것과 같이 XMLA를 사용하여 복원을 완료합니다.  
  
## <a name="restoring-databases-using-xmla"></a>XMLA를 사용하여 데이터베이스 복원  
 XMLA 복원 명령은 .abf 파일을 기반으로 복원을 실행하여 복원 프로세스를 자동화하기 위한 방법입니다. 복원 명령에는 보안 정의, 원격 파티션을 저장할 위치 및 관계형 OLAP(ROLAP) 개체의 재할당을 지정하도록 설정할 수 있는 여러 속성이 있습니다. 자세한 내용은 [Restore 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)를 참조하세요.  
  
> [!IMPORTANT]  
>  복원 명령을 실행하는 사용자는 각 백업 파일에 대해 지정한 백업 위치에서 읽을 수 있는 권한을 가져야 합니다. 서버에 설치되지 않은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 복원하려면 사용자도 해당 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버여야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 덮어쓰려면 사용자가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 복원할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
> [!NOTE]  
>  기존 데이터베이스를 복원한 다음에는 해당 데이터베이스를 복원한 사용자가 보유하고 있는 복원된 데이터베이스 액세스 권한이 손실될 수 있습니다. 이러한 액세스 권한 손실은 백업 수행 당시에 사용자가 서버 역할의 멤버가 아니었거나 모든 권한(관리자)이 있는 데이터베이스 역할의 멤버가 아니었던 경우 발생할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 복원 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](http://msdn.microsoft.com/library/a3990d47-55e2-424e-8eac-87edc937e806)   
 [Analysis Services 데이터베이스 백업 및 복원](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)   
 [Restore 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [데이터베이스 백업, 복원 및 동기화&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
