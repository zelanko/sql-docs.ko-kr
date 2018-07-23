---
title: SQL Server Data Tools 구성 요소 제거 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f8ddb919-661f-4868-8c71-87c96f1f4487
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a3fcb24fc18812b139dfe49376699e83607f16d
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39087545"
---
# <a name="removing-sql-server-data-tools-components"></a>SQL Server Data Tools 구성 요소 제거
SSDT 또는 Visual Studio 제거 시 일부 SSDT(SQL Server Data Tools) 구성 요소는 제거되지 않습니다.  
  
SSDT 또는 Visual Studio 제거 시 다음 Windows Installer 패키지(.msi)는 컴퓨터에서 제거되지 않습니다. 이러한 구성 요소를 제거하면 다른 버전의 Visual Studio가 지원되지 않는 상태가 될 수 있습니다. 구성 요소를 제거하기로 선택하는 경우 Windows 프로그램 추가/제거를 사용합니다.  
  
-   Microsoft SQL Server Data Tools(SSDT.msi)  
  
-   MicrosoftSQL Server Data Tools 빌드 유틸리티(SSDTBuildUtilities.msi)  
  
-   SSDT의 필수 구성 요소(SSDTDBSvcExternals.msi)  
  
다음과 같은 공유 구성 요소는 다른 제품에서 사용할 수 있으며 SSDT를 제거한 후에도 컴퓨터에 그대로 남아 있습니다.  
  
-   SQL Server 데이터 계층 응용 프로그램 프레임워크(DACFramework.msi)  
  
-   SQL Server 관리 개체(SharedManagementObjects.msi)  
  
-   SQL Server Transact\-SQL 언어 서비스(TSqlLanguageService.msi)  
  
-   SQL Server용 Microsoft SQL Server System CLR Types(SQLSysClrTypes.msi)  
  
-   SQL Server Transact\-SQL ScriptDom(SQLDom.msi)  
  
-   SQL Server Transact\-SQL 컴파일러 서비스(SQLLs.msi)  
  
