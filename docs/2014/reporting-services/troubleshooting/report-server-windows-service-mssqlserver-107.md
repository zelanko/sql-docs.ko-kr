---
title: 보고서 서버 Windows 서비스(MSSQLServer) 107 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- MSSQLServer 107 error
ms.assetid: 52b5704b-27f9-400a-a821-d8fa0786afe4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ad8ff3e2a6d87c680c34ae3f2926799e28c3268e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63228992"
---
# <a name="report-server-windows-service-mssqlserver-107"></a>Report Server Windows Service (MSSQLServer) 107
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|107|  
|이벤트 원본|Report Server Windows Service|  
|구성 요소|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|메시지 텍스트|Report Server Windows Service (MSSQLSERVER)에서 보고서 서버 데이터베이스에 연결할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보고서 서버 서비스를 보고서 서버 데이터베이스에 연결할 수 없습니다. 이 오류는 보고서 서버 데이터베이스에 연결할 수 없는 경우 서비스를 다시 시작하면 발생합니다. 이 오류가 발생하는 조건은 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스가 실행되고 있지 않습니다.  
  
-   원격 연결 또는 TCP/IP 프로토콜이 설정되지 않아 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스에 대한 연결이 실패합니다.  
  
-   보고서 서버 데이터베이스가 올바르게 구성되어 있지 않습니다.  
  
-   서비스 계정이 올바르게 구성되어 있지 않거나 계정에 보고서 서버 데이터베이스에 대한 사용 권한이 더 이상 없습니다. 이 조건은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하지 않고 계정 또는 보고서 서버 데이터베이스를 설정한 경우에 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스가 실행되고 있지 않은 경우 해당 서비스를 시작하고 TCP/IP에 대한 원격 연결이 설정되어 있는지 확인합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 보고서 서버 데이터베이스와 서비스 계정을 구성합니다.  
  
## <a name="internal-only"></a>내부 전용  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 서비스 계정 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [보고서 서버 서비스 시작 및 중지](../report-server/start-and-stop-the-report-server-service.md)  
  
  
