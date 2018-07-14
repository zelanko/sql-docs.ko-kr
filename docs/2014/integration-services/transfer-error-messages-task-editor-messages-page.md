---
title: 오류 메시지 전송 태스크 편집기 (메시지 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfererrormessagestask.errormessages.F1
helpviewer_keywords:
- Transfer Error Messages Task Editor
ms.assetid: cb2226a0-3037-4fdf-966f-81eabc0da9cf
caps.latest.revision: 20
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2ee60f4bfe93996ee753f06063bcf7b16aef4d02
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209423"
---
# <a name="transfer-error-messages-task-editor-messages-page"></a>오류 메시지 전송 태스크 편집기(메시지 페이지)
  **오류 메시지 전송 태스크 편집기** 대화 상자의 **메시지** 페이지를 사용하여 하나 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용자 정의 오류 메시지를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 한 인스턴스에서 다른 인스턴스로 복사하기 위한 속성을 지정할 수 있습니다. 이 태스크에 대한 자세한 내용은 [Transfer Error Messages Task](control-flow/transfer-error-messages-task.md)를 참조하십시오.  
  
## <a name="options"></a>변수  
 **SourceConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 원본 서버에 대한 새 연결을 만듭니다.  
  
 **DestinationConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 대상 서버에 대한 새 연결을 만듭니다.  
  
 **IfObjectExists**  
 이름이 동일한 오류 메시지가 이미 대상 서버에 있는 경우 기존 사용자 정의 오류 메시지를 덮어쓸지, 기존 메시지를 건너뛸지, 아니면 태스크가 실패하도록 할지를 선택합니다.  
  
 **TransferAllErrorMessages**  
 원본 서버에서 대상 서버로 모든 사용자 정의 메시지를 복사할지, 아니면 지정한 사용자 정의 메시지만 복사할지를 선택합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**True**|모든 사용자 정의 메시지를 복사합니다.|  
|**False**|지정한 사용자 정의 메시지만 복사합니다.|  
  
 **ErrorMessagesList**  
 복사할 오류 메시지를 선택하려면 찾아보기 단추 **(…)** 를 클릭합니다.  
  
> [!NOTE]  
>  복사할 오류 메시지를 선택하려면 **SourceConnection** 을 지정해야 합니다.  
  
 **ErrorMessageLanguagesList**  
 사용자 정의 오류 메시지를 대상 서버로 복사할 언어를 선택하려면 찾아보기 단추 **(…)** 를 클릭합니다. 다른 언어 버전의 메시지를 대상 서버로 전송하려면 us_english(코드 페이지 1033) 버전의 메시지가 해당 서버에 있어야 합니다.  
  
> [!NOTE]  
>  복사할 오류 메시지를 선택하려면 **SourceConnection** 을 지정해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 태스크](control-flow/integration-services-tasks.md)   
 [오류 메시지 전송 태스크 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [SMO 연결 관리자](connection-manager/smo-connection-manager.md)   
 [오류 메시지 전송 태스크 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [SMO 연결 관리자](connection-manager/smo-connection-manager.md)  
  
  
