---
title: SQL Server 속성(FILESTREAM 페이지) | Microsoft Docs
description: SQL Server의 FILESTREAM 설정을 파악합니다. FILESTREAM을 설정하는 방법과 원격 클라이언트 액세스 및 기타 속성을 구성하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.filestream.f1
helpviewer_keywords:
- FILESTREAM [SQL Server], properties page
ms.assetid: 8a8d38d3-e97a-4b09-a40b-659b2e3a5c47
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 81edbd9bfc913f9d339625a993f866d44e1a313b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730927"
---
# <a name="server-properties---filestream-page"></a>서버 속성 - FILESTREAM 페이지
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 페이지를 사용하여 이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치에 대해 FILESTREAM을 사용하도록 설정할 수 있습니다.  
  
## <a name="ui-element-list"></a>UI 요소 목록  
 **Transact-SQL 액세스에 FILESTREAM 사용**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스에 FILESTREAM을 사용하도록 설정하려면 선택합니다. 다른 컨트롤 옵션을 사용하려면 먼저 이 컨트롤을 선택해야 합니다.  
  
 **파일 I/O 스트리밍 액세스에 FILESTREAM 사용**  
 Win32 스트리밍 액세스에 FILESTREAM을 사용하도록 설정하려면 선택합니다.  
  
 **Windows 공유 이름**  
 FILESTREAM 데이터가 저장될 Windows 공유의 이름을 입력하려면 이 컨트롤을 사용합니다.  
  
 **원격 클라이언트가 FILESTREAM 데이터에 대한 스트리밍 액세스를 가질 수 있도록 허용**  
 원격 클라이언트가 이 서버의 이 FILESTREAM 데이터에 액세스할 수 있도록 허용하려면 이 컨트롤을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
