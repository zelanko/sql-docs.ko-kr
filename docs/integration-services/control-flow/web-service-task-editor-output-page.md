---
title: "웹 서비스 태스크 편집기(출력 페이지) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.webservicestask.output.f1"
helpviewer_keywords: 
  - "웹 서비스 태스크 편집기"
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# 웹 서비스 태스크 편집기(출력 페이지)
  **웹 서비스 태스크 편집기** 대화 상자의 **출력** 페이지를 사용하여 웹 메서드에서 반환하는 결과를 저장할 위치를 지정할 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [웹 서비스 태스크](../../integration-services/control-flow/web-service-task.md)를 참조하세요.  
  
## 정적 옵션  
 **OutputType**  
 결과를 저장할 때 사용할 저장 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**파일 연결**|결과를 파일에 저장합니다. 이 값을 선택하면 동적 옵션 **File**이 표시됩니다.|  
|**변수**|결과를 변수에 저장합니다. 이 값을 선택하면 동적 옵션 **Variable**이 표시됩니다.|  
  
## OutputType 동적 옵션  
  
### OutputType = 파일 연결  
 **파일**  
 목록에서 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### OutputType = 변수  
 **변수**  
 목록에서 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](../Topic/Add%20Variable.md)  
  
## 관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [웹 서비스 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/web-service-task-editor-general-page.md)   
 [웹 서비스 태스크 편집기&#40;입력 페이지&#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
  