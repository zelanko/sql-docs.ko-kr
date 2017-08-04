---
title: "파티션 처리 대상 편집기 (연결 관리자 페이지) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.partprocessingtransformation.connection.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 7add6f82-eed1-47fc-a5d7-7b91f3f24d34
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6ee9df2278b2d143dc1d6373a3da870d31218fe
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="partition-processing-destination-editor-connection-manager-page"></a>파티션 처리 대상 편집기(연결 관리자 페이지)
  **파티션 처리 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 대한 연결을 지정할 수 있습니다.  
  
 파티션 처리 대상에 대한 자세한 내용은 [Partition Processing Destination](../../integration-services/data-flow/partition-processing-destination.md)을 참조하십시오.  
  
> [!NOTE]  
>  여기에서 설명하는 태스크는 Analysis Services 테이블 형식 모델에 적용되지 않습니다.  테이블 형식 모델의 경우 입력 열을 파티션 열에 매핑할 수 없습니다. 대신 [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) 를 사용하여 파티션을 처리할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **Connection manager**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **Analysis Services 연결 관리자 추가** 대화 상자를 사용하면 새 연결을 만들 수 있습니다.  
  
 **사용 가능한 파티션 목록**  
 처리할 파티션을 선택합니다.  
  
 **처리 방법**  
 처리 방법을 선택합니다. 이 옵션의 기본값은 **전체**입니다.  
  
|Value|Description|  
|-----------|-----------------|  
|추가(증분)|파티션의 증분 처리를 수행합니다.|  
|전체|파티션의 전체 처리를 수행합니다.|  
|데이터만|파티션의 업데이트 처리를 수행합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [파티션 처리 대상 편집기 &#40; 매핑 페이지 &#41;](../../integration-services/data-flow/partition-processing-destination-editor-mappings-page.md)   
 [파티션 처리 대상 편집기 &#40; 고급 페이지 &#41;](../../integration-services/data-flow/partition-processing-destination-editor-advanced-page.md)  
  
  
