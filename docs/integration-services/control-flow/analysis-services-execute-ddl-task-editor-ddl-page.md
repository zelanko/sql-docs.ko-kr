---
title: "Analysis Services DDL 실행 태스크 편집기 (DDL 페이지) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL Task Editor
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4bae07f66d84f8a692ad7b59ef61ee63d4a5fd62
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Analysis Services DDL 실행 태스크 편집기(DDL 페이지)
  **Analysis Services DDL 실행 태스크 편집기** 대화 상자의 **DDL** 페이지를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 연결을 지정하고 DDL(데이터 정의 언어) 문의 원본에 대한 정보를 제공할 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)를 참조하십시오.  
  
## <a name="static-options"></a>정적 옵션  
 **연결**  
 선택 된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 클릭 또는 목록에서 연결 관리자 \< **새 연결...** >를 사용 하 고는 **Analysis Services 연결 관리자 추가** 대화 상자는 새 연결을 만듭니다.  
  
 **관련 항목:** [Analysis Services 연결 관리자 추가 대화 상자 UI 참조](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Analysis Services 연결 관리자](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 DDL 문의 원본 유형을 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
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
 목록에서 파일 연결을 선택 하거나 클릭 \< **새 연결...** >를 사용 하 고는 **파일 연결 관리자** 대화 상자는 새 연결을 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md)  
  
### <a name="sourcetype--variable"></a>SourceType = 변수  
 **원본**  
 목록에서 변수를 선택 하거나 클릭 \< **새 변수...** >를 사용 하 고는 **변수 추가** 대화 상자를 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [DDL 작업 편집기 &#40; analysis Services에서 실행 일반 페이지 &#41;](../../integration-services/control-flow/analysis-services-execute-ddl-task-editor-general-page.md)   
 [식 페이지](../../integration-services/expressions/expressions-page.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)   
 [Analysis Services Scripting Language&#40;XMLA용 ASSL&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [XML for Analysis &#40; XMLA &#41; 참조](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
