---
title: 데이터베이스 복원 대화 상자 (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Restore.f1
ms.assetid: a3990d47-55e2-424e-8eac-87edc937e806
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ced766942b0bba6c84985315907708d40565f763
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330423"
---
# <a name="restore-database-dialog-box-analysis-services---multidimensional-data"></a>데이터베이스 복원 대화 상자(Analysis Services - 다차원 데이터)
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 **데이터베이스 복원** 대화 상자를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 백업 파일(.abf) 형식을 사용하는 백업 파일에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 복원할 수 있습니다.  
  
> [!IMPORTANT]  
>  복원 명령을 실행하는 사용자는 각 백업 파일에 대해 지정한 백업 위치에서 읽을 수 있는 권한을 가져야 합니다. 서버에 설치되지 않은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 복원하려면 사용자도 해당 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버여야 합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 덮어쓰려면 사용자가 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 복원할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
> [!NOTE]  
>  기존 데이터베이스를 복원한 다음에는 해당 데이터베이스를 복원한 사용자가 보유하고 있는 복원된 데이터베이스 액세스 권한이 손실될 수 있습니다. 이러한 액세스 권한 손실은 백업 수행 당시에 사용자가 서버 역할의 멤버가 아니었거나 모든 권한(관리자)이 있는 데이터베이스 역할의 멤버가 아니었던 경우 발생할 수 있습니다.  
  
 **데이터베이스 복원 대화 상자를 표시 하려면**  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 **인스턴스의** 데이터베이스 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 폴더 또는 **개체 탐색기**의 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **복원**을 클릭합니다.  
  
 **데이터베이스 복원** 대화 상자에는 다음 페이지가 있습니다.  
  
## <a name="pages"></a>페이지  
 **일반**  
 이 페이지를 사용하여 데이터베이스 복원 중에 사용할 일반 옵션 및 암호를 비롯하여 복원할 데이터베이스, 데이터베이스를 복원할 백업 파일을 선택할 수 있습니다. 이 페이지에 대한 자세한 내용은 [일반&#40;데이터베이스 복원 대화 상자&#41;&#40;Analysis Services - 다차원 데이터&#41;](general-restore-database-dialog-box-analysis-services-multidimensional-data.md)을 참조하세요.  
  
 **파티션**  
 이 페이지를 사용하여 지정한 위치에 로컬 파티션을 복원하고, 원격 백업 파일에서 원격 파티션을 복원할 수 있습니다. 이 페이지에 대한 자세한 내용은 [파티션&#40;데이터베이스 복원 대화 상자&#41;&#40;Analysis Services - 다차원 데이터&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Designers and Dialog Boxes &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Analysis Services 데이터베이스 백업 및 복원](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
