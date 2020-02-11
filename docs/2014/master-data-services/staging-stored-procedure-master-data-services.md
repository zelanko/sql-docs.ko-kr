---
title: 준비 저장 프로시저(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8647a1a4529f7c7d4a8258eac5b726da203c7df9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482721"
---
# <a name="staging-stored-procedure-master-data-services"></a>준비 저장 프로시저(Master Data Services)
  
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 준비 프로세스를 시작할 때는 다음 세 가지 저장 프로시저 중 하나를 사용합니다.  
  
-   stg.udp_name_Leaf  
  
-   stg.udp_name_Consolidated  
  
-   stg.udp_name_Relationship  
  
 여기서 name은 엔터티를 만들 때 지정된 준비 테이블의 이름입니다.  
  
## <a name="staging-process-stored-procedure-parameters"></a>준비 프로세스 저장 프로시저 매개 변수  
 다음 표에서는 이러한 저장 프로시저의 매개 변수를 보여 줍니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|**VersionName**<br /><br /> 필수|버전의 이름입니다. 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 정렬 설정에 따라 대/소문자를 구분할 수도, 그렇지 않을 수도 있습니다.|  
|**LogFlag**<br /><br /> 필수|준비 프로세스 동안 트랜잭션이 기록되는지 여부를 결정합니다. 가능한 값은 다음과 같습니다.<br /><br /> **0**: 트랜잭션을 기록 하지 않습니다.<br />**1**: 트랜잭션 로그<br /><br /> <br /><br /> 트랜잭션에 대한 자세한 내용은 [트랜잭션&#40;Master Data Services&#41;](transactions-master-data-services.md)을 참조하세요.|  
|**BatchTag**<br /><br /> 필수, 웹 서비스에서 사용하는 경우 제외|준비 테이블에 지정된 **BatchTag** 값입니다.|  
|**Batch_ID**<br /><br /> 웹 서비스에만 필요|준비 테이블에 지정된 **Batch_ID** 값입니다.|  
  
### <a name="staging-process-stored-procedure-example"></a>준비 프로세스 저장 프로시저 예  
 다음 예에서는 준비 저장 프로시저를 사용하여 준비 프로세스를 시작하는 방법을 보여 줍니다.  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [유효성 검사 저장 프로시저 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)   
 [준비 프로세스를 사용 하 여 MDS(Master Data Services)에서 멤버 로드 또는 업데이트](add-update-and-delete-data-master-data-services.md)   
 [준비 프로세스 중에 발생 하는 오류를 보려면 MDS(Master Data Services) &#40;&#41;](view-errors-that-occur-during-staging-master-data-services.md)  
  
  
