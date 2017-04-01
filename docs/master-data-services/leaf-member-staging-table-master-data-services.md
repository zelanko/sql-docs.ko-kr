---
title: "리프 멤버 준비 테이블(Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "멤버 준비 테이블 [Master Data Services]"
  - "데이터베이스 [Master Data Services], 멤버 준비 테이블"
ms.assetid: a8c953da-ec20-47dc-8656-ed5f0dfed89b
caps.latest.revision: 14
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 14
---
# 리프 멤버 준비 테이블(Master Data Services)
  리프 멤버 준비 테이블 (stg.name_Leaf)에 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스를 만들고, 업데이트 하 고, 비활성화 하 고, 리프 멤버를 삭제 합니다. 또한 리프 멤버에 대한 특성 값을 업데이트하기 위해 사용할 수도 있습니다.  
  
##  <a name="TableColumns"></a> 테이블 열  
 다음 표에서는 리프 준비 테이블에 나오는 각 필드의 용도에 대해 설명합니다.  
  
|열 이름|설명|값|  
|-----------------|-----------------|------------|  
|**ID**|자동으로 할당된 식별자입니다.|이 필드에 값을 입력하지 마십시오. 일괄 처리를 처리하지 않은 경우 이 필드가 비어 있습니다.|  
|**ImportType**<br /><br /> 필수임|준비된 데이터가 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에 이미 존재하는 데이터와 일치하는 경우 수행할 작업을 결정합니다.|**0**: 새 멤버를 만듭니다. 준비된 데이터가 NULL이 아닌 경우에만 기존 MDS 데이터를 준비된 데이터로 바꿉니다. NULL 값은 무시됩니다. string 특성 값을 NULL로 변경하려면 해당 값을 **~NULL~**로 설정합니다. 숫자 특성 값을 NULL로 바꾸려면로 설정 **-98765432101234567890**합니다. Datetime 특성 값을 NULL로 바꾸려면로 설정 **5555-11-22T12:34:56**합니다.<br /><br /> **1**: 새 멤버만 만듭니다. 기존 MDS 데이터는 업데이트할 수 없습니다.<br /><br /> **2**: 새 멤버를 만듭니다. 기존 MDS 데이터를 준비된 데이터로 바꿉니다. NULL 값을 가져오는 경우 NULL 값이 기존 MDS 값을 덮어씁니다.<br /><br /> **3**: 코드 값을 기반으로 멤버를 비활성화합니다. 모든 특성, 계층 및 컬렉션 멤버 자격, 트랜잭션이 유지 관리되지만 더 이상 UI에서 사용할 수는 없습니다. 멤버가 다른 멤버의 도메인 기반 특성 값으로 사용되는 경우 비활성화할 수 없습니다. 참조 **ImportType5** 대신 합니다.<br /><br /> **4**: 코드 값을 기반으로 멤버를 영구적으로 삭제합니다. 모든 특성, 계층 및 컬렉션 멤버 자격, 트랜잭션이 영구적으로 삭제됩니다. 멤버가 다른 멤버의 도메인 기반 특성 값으로 사용되는 경우 삭제할 수 없습니다. 참조 **ImportType6** 대신 합니다.<br /><br /> **5**: **코드** 값을 기반으로 멤버를 비활성화합니다. 모든 특성, 계층 및 컬렉션 멤버 자격, 트랜잭션이 유지 관리되지만 더 이상 UI에서 사용할 수는 없습니다. 멤버가 다른 멤버의 도메인 기반 특성 값으로 사용되는 경우 관련 값이 NULL로 설정됩니다. ImportType 5는 리프 멤버 전용입니다.<br /><br /> **6**: **코드** 값을 기반으로 멤버를 영구적으로 삭제합니다. 모든 특성, 계층 및 컬렉션 멤버 자격, 트랜잭션이 영구적으로 삭제됩니다. 멤버가 다른 멤버의 도메인 기반 특성 값으로 사용되는 경우 관련 값이 NULL로 설정됩니다. ImportType 6은 리프 멤버 전용입니다.|  
|**ImportStatus_ID**<br /><br /> 필수임|가져오기 프로세스의 상태입니다.|**0**- 레코드를 준비할 수 있음을 나타냅니다.<br /><br /> **1**- 자동으로 할당되며 레코드 준비 프로세스가 성공했음을 나타냅니다.<br /><br /> **2**- 자동으로 할당되며 레코드 준비 프로세스가 실패했음을 나타냅니다.|  
|**Batch_ID**<br /><br /> 웹 서비스에만 필요|준비할 레코드를 그룹화하는 자동 할당 식별자입니다. 일괄 처리의 모든 멤버에는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ID **열의** 사용자 인터페이스에 표시되는 이 식별자가 할당됩니다.|일괄 처리를 처리하지 않은 경우 이 필드가 비어 있습니다.|  
|**BatchTag**<br /><br /> 필수, 웹 서비스에서 사용하는 경우 제외|일괄 처리의 고유 이름으로, 최대 50자입니다.||  
|**ErrorCode**|오류 코드를 표시합니다. 인 모든 레코드는 **ImportStatus_ID** 의 **2**, 참조 [준비 프로세스 오류 및 #40; Master Data Services & #41;](../master-data-services/staging-process-errors-master-data-services.md)합니다.||  
|**코드**<br /><br /> 코드에 대 한 자동으로 생성 될 때를 제외 하 고 필요한 **ImportType1** 또는 **2**; 참조 [자동 코드 생성 및 #40; Master Data Services & #41;](../master-data-services/automatic-code-creation-master-data-services.md) 자세한 내용은|멤버의 고유 코드입니다.||  
|**이름**<br /><br /> 선택 사항|멤버의 이름입니다.||  
|**NewCode**|멤버 코드를 변경하는 경우에만 사용합니다.||  
|\< 특성 이름>|엔터티의 각 특성에 대해 열이 존재합니다. **ImportType** **0** 또는 **2**에 사용합니다. 자유 형식 특성의 경우 특성의 새 텍스트 또는 문자열 값을 지정합니다. 도메인 기반 특성의 경우에는 특성이 될 멤버의 코드를 지정합니다. 링크 특성에 대 한 URL로 시작 해야 **http://**합니다.<br /><br /> 참고: 파일 특성을 준비할 수 없습니다.||  
  
## 참고 항목  
 [개요: 테이블 및 #40;에서 데이터 가져오기 Master Data Services & #41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [준비 및 #40; 중에 발생 하는 오류 보기 Master Data Services & #41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [준비 프로세스 오류 및 #40입니다. Master Data Services & #41;](../master-data-services/staging-process-errors-master-data-services.md)  
  
  