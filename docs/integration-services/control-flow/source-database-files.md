---
title: "원본 데이터베이스 파일 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferdatabasetask.sourcedbfiles.f1
ms.assetid: 7dc6bfeb-37c1-45e8-a705-a87564922265
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0fb66420c0073a79ba6b78608de09fd901c738c0
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="source-database-files"></a>원본 데이터베이스 파일
  **원본 데이터베이스 파일** 대화 상자를 사용하여 원본 서버의 데이터베이스 파일 이름 및 위치를 보거나 데이터베이스 전송 태스크에 대한 네트워크 파일 공유 위치를 지정할 수 있습니다. 이 태스크에 대한 자세한 내용은 [데이터베이스 전송 태스크](../../integration-services/control-flow/transfer-database-task.md)를 참조하세요.  
  
 이 대화 상자를 원본 서버의 데이터베이스 파일 이름 및 위치로 채우려면 먼저 **데이터베이스 전송 태스크 편집기** 대화 상자의 **데이터베이스** 페이지에서 **SourceConnection** 및 **SourceDatabaseName** 을 지정합니다.  
  
## <a name="options"></a>옵션  
 **원본 파일**  
 전송할 원본 서버의 데이터베이스 파일 이름입니다. **원본 파일** 은 읽기 전용입니다.  
  
 **원본 폴더**  
 전송할 데이터베이스 파일이 있는 원본 서버의 폴더입니다. **원본 폴더** 는 읽기 전용입니다.  
  
 **네트워크 파일 공유**  
 데이터베이스 파일을 전송할 원본 서버의 네트워크 공유 폴더입니다. 오프라인 모드에서 데이터베이스를 전송할 때는 **데이터베이스 전송 태스크 편집기** 대화 상자의 **데이터베이스** 페이지에서 **Method** 에 대해 **DatabaseOffline** 을 지정하여 **네트워크 파일 공유** 를 사용합니다.  
  
 네트워크 파일 공유 위치를 입력하거나 찾아보기 단추 **(...)** 를 클릭하여 네트워크 파일 공유 위치를 찾습니다.  
  
 오프라인 모드에서 데이터베이스를 전송할 때는 데이터베이스 파일이 대상 서버에 전송되기 전에 원본 서버의 **네트워크 파일 공유** 위치에 복사됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [데이터베이스 전송 태스크 편집기 &#40; 일반 페이지 &#41;](../../integration-services/control-flow/transfer-database-task-editor-general-page.md)   
 [데이터베이스 전송 태스크 편집기 &#40; 데이터베이스 페이지 &#41;](../../integration-services/control-flow/transfer-database-task-editor-databases-page.md)  
  
  
