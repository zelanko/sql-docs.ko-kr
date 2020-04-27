---
title: 예외 메시지 상자 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- ExceptionMessageBox class, about ExceptionMessageBox class
- exception message box [SQL Server], about exception message box
- exception message box [SQL Server]
- interfaces [SQL Server]
- exceptions [SQL Server]
- messages [SQL Server], exception message box
ms.assetid: 0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 205638b82e8d0d71a3d674bd970e4bf8d2e3ea5f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62753376"
---
# <a name="exception-message-box-programming"></a>예외 메시지 상자 프로그래밍
  예외 메시지 상자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 그래픽 구성 요소와 함께 설치 되 고 사용 되는 프로그래밍 인터페이스입니다. 예외 메시지 상자는 지원 가능한 관리 어셈블리로, 애플리케이션에서 이를 사용하면 메시징 환경을 더욱 효율적으로 제어할 수 있을 뿐 아니라 나중에 참조할 수 있도록 오류 메시지 내용을 저장하고 메시지에 대한 도움말을 찾는 옵션을 사용자에게 제공할 수 있습니다. 예외 메시지 상자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제외한 모든 버전의 [!INCLUDE[ssEW](../../includes/ssew-md.md)]에서 설치되므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 구성 요소가 설치되어 있는 컴퓨터에서 추가 구성 없이 사용할 수 있습니다.  
  
 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 네임스페이스의 <xref:Microsoft.SqlServer.MessageBox> 클래스에는 <xref:System.Windows.Forms.MessageBox> 클래스의 모든 기능뿐 아니라 다른 추가 기능도 있습니다. <xref:System.Windows.Forms.MessageBox>를 사용할 수 있는 모든 태스크에 적합한 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>는 관리 코드 예외를 원활하게 처리하도록 설계되었습니다. 예외 메시지 상자를 사용하여 다음을 수행할 수 있습니다.  
  
-   최대 5개의 단추에 대해 사용자 지정된 단추 텍스트를 제공합니다. 달라진 텍스트 길이에 맞게 단추와 대화 상자의 크기가 자동으로 조정됩니다.  
  
-   사용자가 메시지 제목, 텍스트, 단추 텍스트 및 도움말 링크(있는 경우)를 쉽게 클립보드로 복사하거나 이 정보를 전자 메일 메시지로 보낼 수 있습니다.  
  
-   사용자가 **추가 정보**를 클릭할 때 계층 관계 트리에서 모든 기본 예외 및 오류를 표시 합니다.  
  
-   사용자가 동일한 예외가 다시 발생할 때 메시지를 표시할지 여부를 결정할 수 있습니다.  
  
-   예외와 관련된 도움말 링크를 사용하여 온라인 도움말 시스템에 액세스합니다.  
  
 자세한 내용은 [프로그램 예외 메시지 상자](../../../2014/database-engine/dev-guide/program-exception-message-box.md)를 참조 하세요.  
  
  
