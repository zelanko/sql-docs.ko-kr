---
title: "테이블 (Master Data Services)에서 데이터 가져오기 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ad5b83b1-8e40-4ef8-9ba8-4ea17a58b672
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 47c83a225b97e203875f940a03fe52db80525060
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="import-data-from-tables-master-data-services"></a>테이블에서 데이터 가져오기(Master Data Services)
  데이터를 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]의 모델에 대량으로 추가하고 변경할 수 있습니다.  
  
 **필수 구성 요소**  
  
-   경우에 데이터를 삽입할 수 있는 권한이 있어야\<이름 > _Leaf는 경우\<이름 > _Consolidated의 경우\<이름 > _Relationship 테이블에는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스입니다.  
  
-   stg.udp_ 중 하나를 실행할 수 있는 권한이 있어야\<이름 > _Leaf, stg.udp\_\<이름 > _Consolidated, 또는 stg.udp\_\<이름 > _Relationship 저장 프로시저는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스입니다.  
  
-   모델이 **커밋됨**상태가 아니어야 합니다.  
  
 **[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 데이터를 추가, 업데이트 및 삭제하려면**  
  
1.  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 적절한 준비 테이블로 가져올 구성원을 준비합니다. 예를 들어 필수 필드의 값을 입력합니다. 준비 테이블에 대한 개요는 [개요: 테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)를 참조하세요.  
  
    -   리프 멤버의 경우 테이블은\<이름 > _Leaf, 여기서 \<이름 >의 해당 엔터티를 참조 합니다. 필수 필드에 대한 자세한 내용은 [리프 멤버 준비 테이블&#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)을 참조하세요.  
  
    -   통합된 멤버의 경우 테이블은\<이름 > _Consolidated 합니다. 필수 필드에 대한 자세한 내용은 [통합 멤버 준비 테이블&#40;Master Data Services&#41;](../master-data-services/consolidated-member-staging-table-master-data-services.md)을 참조하세요.  
  
    -   명시적 계층에서 멤버의 위치를 이동, 테이블의 경우는\<이름 > _Relationship 합니다. 필수 필드에 대한 자세한 내용은 [관계 준비 테이블&#40;Master Data Services&#41;](../master-data-services/relationship-staging-table-master-data-services.md)을 참조하세요.  
  
         명시적 계층에서 멤버 이동에 대한 개요는 [개요: 테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)를 참조하세요.  
  
    -   **ImportType** 필드 값을 사용하여 새 구성원을 만드는지, 구성원을 비활성화하는지 또는 구성원을 삭제하는지를 명시합니다. 값에 대한 자세한 내용은 [리프 멤버 준비 테이블&#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md) 및 [통합 멤버 준비 테이블&#40;Master Data Services&#41;](../master-data-services/consolidated-member-staging-table-master-data-services.md)을 참조하세요.  
  
         멤버 비활성화 및 삭제에 대한 개요는 [개요: 테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)를 참조하세요.  
  
2.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 열고 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 데이터베이스 엔진 인스턴스에 연결합니다.  
  
     자세한 내용은 [SQL Server Management Studio](http://msdn.microsoft.com/library/66a6b7b1-de6a-4161-82bd-98ded486947b)를 참조하세요.  
  
3.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 사용하여 준비 테이블로 데이터 가져옵니다.  
  
     자세한 내용은 [SQL Server Import and Export Wizard](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)를 참조하세요.  
  
4.  다음 중 하나를 수행하여 준비 테이블에서 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 테이블로 데이터를 로드합니다.  
  
    -   데이터를 이동하려는 준비 테이블에 해당하는 준비 저장 프로시저를 실행합니다.  
  
         준비 저장 프로시저 및 준비 테이블에 대한 개요는 [개요: 테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)를 참조하세요. 준비 저장 프로시저의 매개 변수에 대한 자세한 내용과 코드 예제는 [준비 저장 프로시저&#40;Master Data Services&#41;](../master-data-services/staging-stored-procedure-master-data-services.md)를 참조하세요.  
  
    -   마스터 데이터 관리의 **통합 관리** 기능 영역을 사용합니다.  
  
         **준비 일괄 처리** 페이지의 드롭다운 목록에서 데이터를 추가할 모델을 선택한 다음 **일괄 처리 시작**을 클릭합니다. 일괄 처리의 상태가 **상태** 필드에 표시됩니다. 상태에 대한 자세한 내용은 [가져오기 상태&#40;Master Data Services&#41;](../master-data-services/import-statuses-master-data-services.md)를 참조하세요.  
  
         ![준비 페이지 마스터 데이터 관리자에서 일괄 처리](../master-data-services/media/mds-stagingbatchespage.png "준비 페이지 마스터 데이터 관리자에서 일괄 처리")  
  
         **의** 준비 일괄 처리 간격 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]설정에 지정된 간격마다 준비 프로세스가 시작됩니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)을 참조하세요.  
  
5.  준비 과정에서 발생한 오류를 봅니다. 자세한 내용은 [준비 과정에서 발생한 오류 보기&#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md) 및 [준비 프로세스 오류&#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)를 참조하세요.  
  
6.  비즈니스 규칙에 대해 데이터의 유효성을 검사합니다.  
  
     마스터 데이터 관리자에서 모델의 **탐색기** 기능 영역으로 이동한 다음 비즈니스 규칙을 적용하여 데이터의 유효성을 검사합니다. 자세한 내용은 [비즈니스 규칙에 대해 특정 멤버 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)를 참조하세요. 저장 프로시저를 사용하여 데이터의 유효성을 검사할 수도 있습니다. 자세한 내용은 [유효성 검사 저장 프로시저&#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)를 참조하세요.  
  
     준비 테이블에서 데이터를 로드하는 경우 비즈니스 규칙에 대해 데이터의 유효성이 자동으로 검사되지 않습니다. 유효성 검사 및 유효성 검사가 발생하는 경우에 대한 자세한 내용은 [유효성 검사&#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)를 참조하세요.  
  
  

