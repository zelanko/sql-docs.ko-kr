---
title: "유효성 검사 저장 프로시저(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 332d3c86-4440-4f12-a6cb-ffbfbccde52c
caps.latest.revision: 8
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 385c5ad267f4a1466cd64c28687da90fbaaabe02
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="validation-stored-procedure-master-data-services"></a>유효성 검사 저장 프로시저(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 버전의 유효성을 검사하여 모델 버전의 모든 멤버에 비즈니스 규칙을 적용할 수 있습니다.  
  
 이 항목에서는 **mdm.udpValidateModel** 저장 프로시저를 사용하여 데이터의 유효성을 검사하는 방법에 대해 설명합니다. [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램에서 관리자는 UI에서 유효성 검사를 수행할 수 있습니다. 자세한 내용은 [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)를 참조하세요.  
  
> [!NOTE]  
>  준비 프로세스 완료 전에 유효성 검사를 호출하는 경우, 준비 프로세스가 완료되지 않은 멤버는 유효성 검사가 되지 않습니다.  
  
## <a name="example"></a>예제  
  
```  
DECLARE @ModelName nVarchar(50) = 'Customer'   
DECLARE @Model_id int   
DECLARE @UserName nvarchar(50)= 'DOMAIN\user_name'   
DECLARE @User_ID int   
DECLARE @Version_ID int   
  
SET @User_ID = (SELECT ID    
                 FROM mdm.tblUser u   
                 WHERE u.UserName = @UserName)   
SET @Model_ID = (SELECT Top 1 Model_ID   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_Name = @ModelName)   
SET @Version_ID = (SELECT MAX(ID)   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_ID = @Model_ID)  
  
EXECUTE mdm.udpValidateModel @User_ID, @Model_ID, @Version_ID, 1  
  
```  
  
## <a name="parameters"></a>매개 변수  
 이 프로시저의 매개 변수는 다음과 같습니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|UserID|사용자 ID입니다.|  
|Model_ID|모델 ID입니다.|  
|Version_ID|버전 ID입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [개요: 테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
  
