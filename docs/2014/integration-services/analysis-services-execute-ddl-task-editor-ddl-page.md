---
title: Analysis Services DDL 실행 태스크 편집기 (DDL 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL Task Editor
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e8f07c94b986c697721188a50e2ec5d478ac0b1b
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146859"
---
# <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Analysis Services DDL 실행 태스크 편집기(DDL 페이지)
  **Analysis Services DDL 실행 태스크 편집기** 대화 상자의 **DDL** 페이지를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트 또는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 대한 연결을 지정하고 DDL(데이터 정의 언어) 문의 원본에 대한 정보를 제공할 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md)를 참조하십시오.  
  
## <a name="static-options"></a>정적 옵션  
 **대량 삽입 태스크 편집기**  
 목록에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트 또는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭한 다음 **Analysis Services 연결 관리자 추가** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **관련 항목:** [Analysis Services 연결 관리자 추가 대화 상자 UI 참조](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Analysis Services 연결 관리자](connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 DDL 문의 원본 유형을 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 **SourceDirect** 입력란에 저장된 DDL 문으로 설정합니다. 이 값을 선택하면 다음 섹션에 동적 옵션이 표시됩니다.|  
|**파일 연결**|원본을 DDL 문이 포함된 파일로 설정합니다. 이 값을 선택하면 다음 섹션에 동적 옵션이 표시됩니다.|  
|**변수**|원본을 변수로 설정합니다. 이 값을 선택하면 다음 섹션에 동적 옵션이 표시됩니다.|  
  
## <a name="dynamic-options"></a>동적 옵션  
  
### <a name="sourcetype--direct-input"></a>SourceType = 직접 입력  
 **원본**  
 DDL 문을 입력하거나 줄임표 **(…)** 를 클릭한 다음 **DDL 문** 대화 상자에 문을 입력합니다.  
  
### <a name="sourcetype--file-connection"></a>SourceType = 파일 연결  
 **원본**  
 목록에서 파일 연결을 선택하거나 \<**새 연결...**>을 클릭한 다음 **파일 연결 관리자** 대화 상자를 사용하여 새 연결을 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md)  
  
### <a name="sourcetype--variable"></a>SourceType = 변수  
 **원본**  
 목록에서 변수를 선택하거나 \<**새 변수...**>를 클릭한 다음 **변수 추가** 대화 상자를 사용하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md)  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services DDL 실행 태스크 편집기&#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [식 페이지](expressions/expressions-page.md)   
 [제어 흐름](control-flow/control-flow.md)   
 [Analysis Services Scripting Language &#40;ASSL&#41; 참조](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [XMLA&#40;XML for Analysis&#41; 참조](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)  
  
  
