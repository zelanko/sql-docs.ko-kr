---
title: Master 저장된 프로시저 전송 태스크 편집기 (일반 페이지) | Microsoft Docs
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
- sql12.dts.designer.transferstoredprocedurestask.general.f1
helpviewer_keywords:
- Transfer Stored Procedures Task Editor
ms.assetid: fa1abd4c-e2be-427f-be53-860e49c97227
caps.latest.revision: 24
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f89c6e35e69b8982b379b61e5341e80d6f768cd9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205793"
---
# <a name="transfer-master-stored-procedures-task-editor-general-page"></a>master 저장 프로시저 전송 태스크 편집기(일반 페이지)
  **master 저장 프로시저 전송 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 master 저장 프로시저 전송 태스크의 이름을 지정하고 해당 태스크를 설명할 수 있습니다. 이 태스크에 대한 자세한 내용은 [Transfer Master Stored Procedures Task](control-flow/transfer-master-stored-procedures-task.md)를 참조하십시오.  
  
> [!NOTE]  
>  이 태스크는 **dbo** 소유의 사용자 정의 저장 프로시저만 원본 서버의 **master** 데이터베이스에서 대상 서버의 **master** 데이터베이스로 전송합니다. 대상 서버의 **master** 데이터베이스에서 CREATE PROCEDURE 권한을 부여받았거나 대상 서버에서 **sysadmin** 고정 서버 역할의 멤버인 사용자만 해당 데이터베이스에 저장 프로시저를 만들 수 있습니다.  
  
## <a name="options"></a>변수  
 **이름**  
 master 저장 프로시저 전송 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 master 저장 프로시저 전송 태스크에 대한 설명을 입력합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 태스크](control-flow/integration-services-tasks.md)   
 [master 저장 프로시저 전송 태스크 편집기&#40저장 프로시저 페이지&#41;](../../2014/integration-services/transfer-master-stored-procedures-task-editor-stored-procedures-page.md)   
 [식 페이지](expressions/expressions-page.md)  
  
  
