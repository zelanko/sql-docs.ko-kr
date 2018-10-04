---
title: 대상 데이터베이스 파일 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.destdbfiles.f1
ms.assetid: f6f90417-86fb-4b8c-a790-0b215c344ef6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fb6f834ab26fb6d5cc7535d217745af92e97c2a5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135280"
---
# <a name="destination-database-files"></a>대상 데이터베이스 파일
  **대상 데이터베이스 파일** 대화 상자를 사용하여 대상 서버의 데이터베이스 파일 이름 및 위치를 확인 또는 변경하거나 데이터베이스 전송 태스크에 대한 네트워크 파일 위치를 지정할 수 있습니다. 이 태스크에 대한 자세한 내용은 [데이터베이스 전송 태스크](control-flow/transfer-database-task.md)를 참조하세요.  
  
 이 대화 상자를 원본 서버의 데이터베이스 파일 이름 및 위치로 자동으로 채우려면 먼저 **데이터베이스 전송 태스크 편집기**대화 상자의 **데이터베이스**페이지에서 **SourceConnection** , **SourceDatabaseName** 및 **SourceDatabaseFiles** 를 지정합니다.  
  
## <a name="options"></a>변수  
 **대상 파일**  
 전송된 대상 서버의 데이터베이스 파일 이름입니다.  
  
 파일 이름을 입력하거나 파일 이름을 클릭하여 편집합니다.  
  
 **대상 폴더**  
 데이터베이스 파일을 전송할 대상 서버의 폴더입니다.  
  
 폴더 경로를 입력하거나, 폴더 경로를 클릭하여 편집하거나, 찾아보기를 클릭하여 대상 서버의 데이터베이스 파일을 전송할 폴더를 찾습니다.  
  
 **네트워크 파일 공유**  
 데이터베이스 파일을 전송할 대상 서버의 네트워크 공유 폴더입니다. 오프라인 모드에서 데이터베이스를 전송할 때는 **데이터베이스 전송 태스크 편집기** 대화 상자의 **데이터베이스** 페이지에서 **Method** 에 대해 **DatabaseOffline** 을 지정하여 **네트워크 파일 공유** 를 사용합니다.  
  
 네트워크 파일 공유 위치를 입력하거나 찾아보기를 클릭하여 네트워크 파일 공유 위치를 찾습니다.  
  
 오프라인 모드에서 데이터베이스를 전송할 때는 데이터베이스 파일이 **대상 폴더** 위치에 전송되기 전에 **네트워크 파일 공유** 위치에 복사됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [데이터베이스 전송 태스크 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [데이터베이스 전송 태스크 편집기 &#40;페이지를 데이터베이스&#41;](../../2014/integration-services/transfer-database-task-editor-databases-page.md)  
  
  
