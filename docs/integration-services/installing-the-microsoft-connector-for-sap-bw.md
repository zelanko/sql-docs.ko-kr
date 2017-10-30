---
title: "Microsoft Connector for SAP BW 설치 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 663ae1f9c71987729b96510157ce39868490f00b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="installing-the-microsoft-connector-for-sap-bw"></a>Microsoft Connector for SAP BW 설치
  SQL Server 2016용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW는 SQL Server 2016 기능 팩의 구성 요소입니다. Connector for SAP BW 및 해당 설명서를 설치하려면 [SQL Server 2016 기능 팩 웹 페이지](http://go.microsoft.com/fwlink/?LinkId=746297)에서 설치 관리자를 다운로드하여 실행하세요.  
  
> [!IMPORTANT]  
>  Microsoft Connector for SAP BW 설명서에서는 사용자가 SAP Netweaver BW 환경에 대해 잘 알고 있다고 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP Netweaver BW에서 데이터를 추출하려면 추가 SAP 라이선스가 필요합니다. SAP에서 이러한 요구 사항을 확인하십시오.  
  
## <a name="required-sap-files"></a>필요한 SAP 파일  
 SAP BW용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector를 사용하기 위해 로컬 컴퓨터에 SAP Front End 소프트웨어(SAP GUI)를 설치할 필요는 없습니다.  
  
 하지만 SAP .NET 커넥터 파일 librfc32.dll을 Windows 폴더의 system 하위 폴더에 복사해야 합니다. 일반적으로 이 폴더 위치는 **C:\Windows\system32**입니다.  
  
## <a name="considerations-for-64-bit-computers"></a>64비트 컴퓨터에 대한 고려 사항  
 SAP BW용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector는 64비트 버전의 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows를 완전히 지원합니다. 64비트 컴퓨터의 SAP BW용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector에는 다음과 같은 추가 요구 사항이 있습니다.  
  
-   64비트 Windows 운영 체제에서 패키지를 64비트 모드로 실행하려면 SAP GUI 파일 librfc32.dll의 64비트 버전을 Windows 폴더의 **system32** 폴더에 복사합니다. 일반적으로 이 파일 위치는 **C:\Windows\system32**입니다.  
  
-   64비트 Windows 운영 체제에서 패키지를 32비트 모드로 실행하려면 SAP GUI 파일 librfc32.dll을 Windows 폴더의 **SysWow64** 폴더에 복사합니다. 일반적으로 이 폴더 위치는 **C:\Windows\SysWow64**입니다.  
  
  

