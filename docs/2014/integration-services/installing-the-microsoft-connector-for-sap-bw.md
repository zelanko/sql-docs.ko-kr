---
title: Microsoft Connector for 1.1 SAP BW 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: dc6bbbf5972615880d3852d5f56a955862c9f22b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186124"
---
# <a name="installing-the-microsoft-connector-for-11-sap-bw"></a>Microsoft Connector for 1.1 SAP BW 설치
  SAP BW용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 및 해당 설명서를 설치하려면 SQL Server 기능 팩 웹 페이지에서 Windows Installer 패키지를 다운로드하고 실행합니다.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP Netweaver BW에서 데이터를 추출하려면 추가 SAP 라이선스가 필요합니다. SAP에서 이러한 요구 사항을 확인하십시오.  
  
## <a name="required-sap-files"></a>필요한 SAP 파일  
 SAP BW용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1을 사용하기 위해서는 로컬 컴퓨터에 SAP Front End 소프트웨어(SAP GUI)를 설치할 필요가 없습니다.  
  
 하지만 SAP .NET 커넥터 파일 librfc32.dll을 Windows 폴더의 system 하위 폴더에 복사해야 합니다. 일반적으로 이 폴더 위치는 **C:\Windows\system32**입니다.  
  
## <a name="considerations-for-64-bit-computers"></a>64비트 컴퓨터에 대한 고려 사항  
 SAP BW용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1은 64비트 버전의 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows를 완전히 지원합니다. 64비트 컴퓨터에서 SAP BW용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1은 다음과 같은 추가 요구 사항이 있습니다.  
  
-   64비트 Windows 운영 체제에서 패키지를 64비트 모드로 실행하려면 SAP GUI 파일 librfc32.dll의 64비트 버전을 Windows 폴더의 **system32** 폴더에 복사합니다. 일반적으로 이 파일 위치는 **C:\Windows\system32**입니다.  
  
-   64비트 Windows 운영 체제에서 패키지를 32비트 모드로 실행하려면 SAP GUI 파일 librfc32.dll을 Windows 폴더의 **SysWow64** 폴더에 복사합니다. 일반적으로 이 폴더 위치는 **C:\Windows\SysWow64**입니다.  
  
  