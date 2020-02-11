---
title: 서버에 연결(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connectoserverunknownservertype.f1
- sql12.swb.connection.login.sqlserver.f1
- sql12.swb.connection.login.sqlce.f1
- sql12.swb.manageSS2k.f1
- sql12.swb.connecttoce.f1
- sql12.swb.connecttoce.connectionproperties.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 018ca302bf4d5fe8271369008ffbfec7d228cfbf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63245738"
---
# <a name="connect-to-server-database-engine"></a>서버에 연결(데이터베이스 엔진)
  에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]연결할 때이 대화 상자를 사용 하 여 옵션을 확인 하거나 지정할 수 있습니다. 대부분의 경우 **서버 이름** 상자에서 데이터베이스 서버의 컴퓨터 이름을 입력한 다음 **연결**을 클릭하여 연결할 수 있습니다. 
  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]에 연결하는 경우 컴퓨터 이름과 그 뒤에 **\sqlexpress**를 사용합니다.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하는 데 다양한 요인이 영향을 줄 수 있습니다.  
  
## <a name="options"></a>옵션  
 **서버 유형**  
 개체 탐색기에서 서버를 등록하는 경우 연결할 서버 유형을 [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]중에서 선택합니다. 대화 상자의 나머지 부분에는 선택한 서버 유형에 적용되는 옵션만 표시됩니다. 등록된 서버에서 서버를 등록하는 경우 **서버 유형** 상자는 읽기 전용이며 등록된 서버 구성 요소에 표시된 서버 유형과 일치합니다. 다른 유형의 서버를 등록하려면 새 서버를 등록하기 전에 등록된 서버 도구 모음에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssEW](../../includes/ssew-md.md)]또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 중에서 선택합니다.  
  
 **서버 이름**  
 연결할 서버 인스턴스를 선택합니다. 마지막으로 연결한 서버 인스턴스가 기본적으로 표시됩니다.  
  
> [!NOTE]  
>  
  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 의 활성 사용자 인스턴스에 연결하려면 np:\\\\.\pipe\3C3DF6B1-2262-47\tsql\query와 같이 파이프 이름을 지정하는 명명된 파이프 프로토콜을 사용하여 연결합니다. 자세한 내용은 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 설명서를 참조하세요.  
  
 **인증**  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결할 때는 두 가지 인증 모드를 사용할 수 있습니다.  
  
 **Windows 인증 모드(Windows 인증)**  
 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증 모드에서는 사용자가 Windows 사용자 계정을 통해 연결할 수 있습니다.  
  
 **SQL Server 인증**  
 사용자가 지정한 로그인 이름과 암호를 사용하여 트러스트되지 않은 연결로부터 연결하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정이 설정되고 지정한 암호가 전에 기록한 암호와 일치하는지를 확인하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 자체적으로 인증을 수행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 로그인 계정이 설정되어 있지 않으면 인증이 실패하고 오류 메시지가 나타납니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요.  
  
 **사용자 이름**  
 연결에 사용할 사용자 이름을 입력합니다. 이 옵션은 Windows 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다.  
  
 **로그인**  
 연결 시 사용할 로그인을 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다.  
  
 **암호**  
 로그인 암호를 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 편집할 수 있습니다.  
  
 **연결**  
 위에서 선택한 서버에 연결하려면 클릭합니다.  
  
 **옵션**  
 서버 등록, 암호 저장 등의 추가 서버 연결 옵션을 표시하려면 클릭합니다.  
  
  
