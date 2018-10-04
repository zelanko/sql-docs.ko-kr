---
title: 웹 서비스 태스크 편집기 (출력 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e2a0c1639352b8c5aaad9be4bd6740eceacb6cf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132013"
---
# <a name="web-service-task-editor-output-page"></a>웹 서비스 태스크 편집기(출력 페이지)
  **웹 서비스 태스크 편집기** 대화 상자의 **출력** 페이지를 사용하여 웹 메서드에서 반환하는 결과를 저장할 위치를 지정할 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [웹 서비스 태스크](control-flow/web-service-task.md)를 참조하세요.  
  
## <a name="static-options"></a>정적 옵션  
 **OutputType**  
 결과를 저장할 때 사용할 저장 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 연결**|결과를 파일에 저장합니다. 이 값을 선택하면 동적 옵션 **File**이 표시됩니다.|  
|**변수**|결과를 변수에 저장합니다. 이 값을 선택하면 동적 옵션 **Variable**이 표시됩니다.|  
  
## <a name="outputtype-dynamic-options"></a>OutputType 동적 옵션  
  
### <a name="outputtype--file-connection"></a>OutputType = 파일 연결  
 **최근에 사용한 파일**  
 목록에서 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="outputtype--variable"></a>OutputType = 변수  
 **변수**  
 목록에서 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [웹 서비스 태스크 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [웹 서비스 태스크 편집기 &#40;페이지를 입력 합니다.&#41;](../../2014/integration-services/web-service-task-editor-input-page.md)   
 [식 페이지](expressions/expressions-page.md)  
  
  
