---
title: "대상 데이터베이스 파일 | Microsoft Docs"
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
  - "sql13.dts.designer.transferdatabasetask.destdbfiles.f1"
ms.assetid: f6f90417-86fb-4b8c-a790-0b215c344ef6
caps.latest.revision: 16
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# 대상 데이터베이스 파일
  **대상 데이터베이스 파일** 대화 상자를 사용하여 대상 서버의 데이터베이스 파일 이름 및 위치를 확인 또는 변경하거나 데이터베이스 전송 태스크에 대한 네트워크 파일 위치를 지정할 수 있습니다. 이 태스크에 대한 자세한 내용은 [데이터베이스 전송 태스크](../../integration-services/control-flow/transfer-database-task.md)를 참조하세요.  
  
 이 대화 상자를 원본 서버의 데이터베이스 파일 이름 및 위치로 자동으로 채우려면 먼저 **데이터베이스 전송 태스크 편집기**대화 상자의 **데이터베이스**페이지에서 **SourceConnection** , **SourceDatabaseName** 및 **SourceDatabaseFiles** 를 지정합니다.  
  
## 옵션  
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
  
## 관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [데이터베이스 전송 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/transfer-database-task-editor-general-page.md)   
 [데이터베이스 전송 태스크 편집기&#40;데이터베이스 페이지&#41;](../../integration-services/control-flow/transfer-database-task-editor-databases-page.md)  
  
  