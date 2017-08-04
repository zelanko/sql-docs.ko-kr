---
title: "준비 저장된 프로시저 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
caps.latest.revision: 15
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c2c12151d25b7d563a8a37a7ccfd617bca5cb479
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="staging-stored-procedure-master-data-services"></a>준비 저장 프로시저(Master Data Services)
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 준비 프로세스를 시작할 때는 다음 세 가지 저장 프로시저 중 하나를 사용합니다.  
  
-   stg.udp_\<이름 > _Leaf  
  
-   stg.udp_\<이름 > _Consolidated  
  
-   stg.udp_\<이름 > _Relationship  
  
 여기서 name은 엔터티를 만들 때 지정된 준비 테이블의 이름입니다.  
  
## <a name="staging-process-stored-procedure-parameters"></a>준비 프로세스 저장 프로시저 매개 변수  
 다음 표에서는 이러한 저장 프로시저의 매개 변수를 보여 줍니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|**VersionName**<br /><br /> 필수임|버전의 이름입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 정렬 설정에 따라 대/소문자를 구분할 수도, 그렇지 않을 수도 있습니다.|  
|**LogFlag**<br /><br /> 필수임|준비 프로세스 동안 트랜잭션이 기록되는지 여부를 결정합니다. 가능한 값은<br /><br /> **0**: 트랜잭션을 기록하지 않습니다.<br /><br /> **1**: 트랜잭션을 기록합니다.<br /><br /> <br /><br /> 트랜잭션에 대한 자세한 내용은 [트랜잭션&#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)을 참조하세요.|  
|**BatchTag**<br /><br /> 필수, 웹 서비스에서 사용하는 경우 제외|준비 테이블에 지정된 **BatchTag** 값입니다.|  
|**Batch_ID**<br /><br /> 웹 서비스에만 필요|준비 테이블에 지정된 **Batch_ID** 값입니다.|  
|**사용자 이름**|선택적 매개 변수|  
|**사용자 ID**|선택적 매개 변수|  
  
### <a name="staging-process-stored-procedure-example"></a>준비 프로세스 저장 프로시저 예  
 다음 예에서는 준비 저장 프로시저를 사용하여 준비 프로세스를 시작하는 방법을 보여 줍니다.  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
      @UserName=N’domain\user’  
  
GO  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [유효성 검사 저장 프로시저&#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [준비 과정에서 발생하는 오류 보기&#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)  
  
  

