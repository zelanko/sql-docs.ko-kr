---
title: "FTP 태스크 편집기(파일 전송 페이지) | Microsoft Docs"
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
  - "sql13.dts.designer.ftptask.filetransfer.f1"
helpviewer_keywords: 
  - "파일 전송 프로토콜 태스크 편집기"
ms.assetid: 37e52220-feb2-474c-ad88-fa1b1059acd4
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# FTP 태스크 편집기(파일 전송 페이지)
  **FTP 태스크 편집기** 대화 상자의 **파일 전송** 페이지를 사용하여 태스크에서 수행할 FTP 작업을 구성할 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [FTP 태스크](../../integration-services/control-flow/ftp-task.md)를 참조하세요.  
  
## 옵션  
 **IsRemotePathVariable**  
 원격 경로가 변수에 저장되는지 여부를 나타냅니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|대상 경로가 변수에 저장됩니다. 이 값을 선택하면 동적 옵션 **RemoteVariable**이 표시됩니다.|  
|**False**|파일 연결 관리자에서 대상 경로를 지정합니다. 이 값을 선택하면 동적 옵션 **RemotePath**가 표시됩니다.|  
  
 **OverwriteFileAtDestination**  
 대상 파일을 덮어쓸 수 있는지 여부를 지정합니다.  
  
 **IsLocalPathVariable**  
 로컬 경로가 변수에 저장되는지 여부를 나타냅니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|대상 경로가 변수에 저장됩니다. 이 값을 선택하면 동적 옵션 **LocalVariable**이 표시됩니다.|  
|**False**|파일 연결 관리자에서 대상 경로를 지정합니다. 이 값을 선택하면 동적 옵션 **LocalPath**가 표시됩니다.|  
  
 **연산**  
 수행할 FTP 작업을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**파일 보내기**|파일을 보냅니다. 이 값을 선택하면 동적 옵션 **LocalVariable**, **LocalPathRemoteVariable** 및 **RemotePath**가 표시됩니다.|  
|**파일 받기**|파일을 받습니다. 이 값을 선택하면 동적 옵션 **LocalVariable**, **LocalPathRemoteVariable** 및 **RemotePath**가 표시됩니다.|  
|**로컬 디렉터리 만들기**|로컬 디렉터리를 만듭니다. 이 값을 선택하면 동적 옵션 **LocalVariable** 및 **LocalPath**가 표시됩니다.|  
|**원격 디렉터리 만들기**|원격 디렉터리를 만듭니다. 이 값을 선택하면 동적 옵션 **RemoteVariable** 및 **RemotePath**가 표시됩니다.|  
|**로컬 디렉터리 제거**|로컬 디렉터리를 제거합니다. 이 값을 선택하면 동적 옵션 **LocalVariable** 및 **LocalPath**가 표시됩니다.|  
|**원격 디렉터리 제거**|원격 디렉터리를 제거합니다. 이 값을 선택하면 동적 옵션 **RemoteVariable** 및 **RemotePath**가 표시됩니다.|  
|**로컬 파일 삭제**|로컬 파일을 삭제합니다. 이 값을 선택하면 동적 옵션 **LocalVariable** 및 **LocalPath**가 표시됩니다.|  
|**원격 파일 삭제**|원격 파일을 삭제합니다. 이 값을 선택하면 동적 옵션 **RemoteVariable** 및 **RemotePath**가 표시됩니다.|  
  
 **IsTransferASCII**  
 원격 FTP 서버와 파일을 주고 받을 때 ASCII 모드로 파일을 전송할지 여부를 나타냅니다.  
  
## IsRemotePathVariable 동적 옵션  
  
### IsRemotePathVariable = True  
 **RemoteVariable**  
 기존 사용자 정의 변수를 선택하거나 \<**새 변수...**>를 클릭하여 사용자 정의 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), 변수 추가  
  
### IsRemotePathVariable = False  
 **RemotePath**  
 기존 FTP 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 연결 관리자를 만듭니다.  
  
 **관련 항목**: [FTP 연결 관리자](../../integration-services/connection-manager/ftp-connection-manager.md), [FTP 연결 관리자 편집기](../../integration-services/connection-manager/ftp-connection-manager-editor.md)  
  
## IsLocalPathVariable 동적 옵션  
  
### IsLocalPathVariable = True  
 **LocalVariable**  
 기존 사용자 정의 변수를 선택하거나 \<**새 변수...**>를 클릭하여 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), 변수 추가  
  
### IsLocalPathVariable = False  
 **LocalPath**  
 기존 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 연결 관리자를 만듭니다.  
  
 **관련 항목**: [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## 관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [FTP 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/ftp-task-editor-general-page.md)   
 [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
  