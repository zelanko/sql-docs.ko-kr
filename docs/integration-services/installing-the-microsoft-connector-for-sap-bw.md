---
description: Microsoft Connector for SAP BW 설치
title: Microsoft Connector for SAP BW 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3244ffbd690d7f2ea79862eb1963df60607ac2d6
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384642"
---
# <a name="installing-the-microsoft-connector-for-sap-bw"></a>Microsoft Connector for SAP BW 설치

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  SQL Server 2016용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW는 SQL Server 2016 기능 팩의 구성 요소입니다. Connector for SAP BW 및 해당 설명서를 설치하려면 [SQL Server 2016 기능 팩 웹 페이지](https://www.microsoft.com/download/details.aspx?id=56833)에서 설치 관리자를 다운로드하여 실행하세요.  

> [!IMPORTANT]
> Microsoft는 업데이트된 버전의 SAP BW용 커넥터를 제공하지 않습니다. Microsoft는 타사에서 개발된 SAP BW용 소스 코드 구성 요소를 소유하지 않으며 결과적으로 업데이트할 수 없습니다. [Theobald Software](https://theobald-software.com/en/xtract-is-productinfo.html) 등 Microsoft ISV 파트너로부터 최신 SAP 연결 구성 요소를 구매하는 것이 좋습니다. Microsoft의 ISV 파트너는 Azure에서 설치하기 위한 SSIS용 SAP 연결 구성 요소를 적용했습니다.

> [!IMPORTANT]  
>  Microsoft Connector for SAP BW 설명서에서는 사용자가 SAP Netweaver BW 환경에 대해 잘 알고 있다고 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
> [!IMPORTANT]  
>  SAP Netweaver BW에서 데이터를 추출하려면 추가 SAP 라이선스가 필요합니다. SAP에서 이러한 요구 사항을 확인하십시오.  
  
## <a name="required-sap-files"></a>필요한 SAP 파일  
 SAP BW용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector를 사용하기 위해 로컬 컴퓨터에 SAP Front End 소프트웨어(SAP GUI)를 설치할 필요는 없습니다.  
  
 하지만 SAP .NET 커넥터 파일 librfc32.dll을 Windows 폴더의 system 하위 폴더에 복사해야 합니다. 일반적으로 이 폴더 위치는 **C:\Windows\system32** 입니다.  
  
## <a name="considerations-for-64-bit-computers"></a>64비트 컴퓨터에 대한 고려 사항  
 SAP BW용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector는 64비트 버전의 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows를 완전히 지원합니다. 64비트 컴퓨터의 SAP BW용 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector에는 다음과 같은 추가 요구 사항이 있습니다.  
  
-   64비트 Windows 운영 체제에서 패키지를 64비트 모드로 실행하려면 SAP GUI 파일 librfc32.dll의 64비트 버전을 Windows 폴더의 **system32** 폴더에 복사합니다. 일반적으로 이 파일 위치는 **C:\Windows\system32** 입니다.  
  
-   64비트 Windows 운영 체제에서 패키지를 32비트 모드로 실행하려면 SAP GUI 파일 librfc32.dll을 Windows 폴더의 **SysWow64** 폴더에 복사합니다. 일반적으로 이 폴더 위치는 **C:\Windows\SysWow64** 입니다.  
  
  
