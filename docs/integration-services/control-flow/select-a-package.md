---
description: 패키지 선택
title: 패키지 선택 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.selectapackage.f1
helpviewer_keywords:
- Select a Package dialog box
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ce10dbf39c92754b2fbc2879041e98094dc06ceb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88349939"
---
# <a name="select-a-package"></a>패키지 선택

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **패키지 선택** 대화 상자를 사용하여 메시지 큐 태스크에서 수신할 메시지를 전송하는 패키지를 지정할 수 있습니다.  
  
## <a name="static-options"></a>정적 옵션  
 **위치**  
 패키지의 위치를 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|위치를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 설정합니다. 이 값을 선택하면 동적 옵션 **서버**, **Windows 인증 사용**, **SQL Server 인증 사용**, **사용자 이름**및 **암호**가 표시됩니다.|  
|DTSX 파일|위치를 DTSX 파일로 설정합니다. 이 값을 선택하면 동적 옵션 **파일 이름**이 표시됩니다.|  
  
## <a name="location-dynamic-options"></a>Location 동적 옵션  
  
### <a name="location--sql-server"></a>Location = SQL Server  
 **패키지 이름**  
 지정한 서버에 저장된 패키지를 선택합니다.  
  
 **Server**  
 서버 이름을 입력하거나 목록에서 서버를 선택합니다.  
  
 **Windows 인증 사용**  
 Windows 인증을 사용하려면 클릭합니다.  
  
 **SQL Server 인증 사용**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하려면 클릭합니다.  
  
 **사용자 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 서버에 로그온할 때 사용할 사용자 이름을 입력합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 암호를 입력합니다.  
  
### <a name="location--dtsx-file"></a>위치 = DTSX 파일  
 **파일 이름**  
 패키지 경로를 입력하거나 찾아보기 단추 **(...)** 를 클릭하고 패키지를 찾습니다.  
  
## <a name="see-also"></a>관련 항목  
 [메시지 큐 태스크](../../integration-services/control-flow/message-queue-task.md)  
  
  
