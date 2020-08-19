---
description: DCOM에서 실행하도록 DLL 사용
title: DLL을 DCOM에서 실행할 수 있도록 설정 Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
author: rothja
ms.author: jroth
ms.openlocfilehash: d685e03834b1c8390ddd51a8e590f25cd6307efe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452205"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>DCOM에서 실행하도록 DLL 사용
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 다음 단계에서는 구성 요소 서비스를 통해 DCOM과 Microsoft 인터넷 정보 서비스 (HTTP)를 둘 다 사용 하도록 비즈니스 개체 .dll을 설정 하는 방법을 간략하게 설명 합니다.  
  
1.  구성 요소 서비스 MMC 스냅인에서 비어 있는 새 패키지를 만듭니다.  
  
     구성 요소 서비스 MMC 스냅인을 사용 하 여 패키지를 만들고이 패키지에 DLL을 추가 합니다. 이렇게 하면 DCOM을 통해 .dll에 액세스할 수 있지만 IIS를 통해 접근성을 제거 합니다. .Dll에 대 한 레지스트리를 체크 인하면 **inproc** 키가 비어 있게 됩니다 .이 항목의 뒷부분에 설명 된 활성화 특성을 설정 하면 **inproc** 키에 값이 추가 됩니다.  
  
2.  패키지에 비즈니스 개체를 설치 합니다.  
  
     또는  
  
     [RDSServer DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체를 패키지에 가져옵니다.  
  
3.  **작성자의 프로세스** (라이브러리 응용 프로그램)에서 패키지에 대 한 활성화 특성을로 설정 합니다.  
  
     동일한 컴퓨터의 DCOM 및 IIS를 통해 .dll을 액세스할 수 있도록 구성 요소 서비스 MMC 스냅인에서 구성 요소의 활성화 특성을 설정 해야 합니다. **작성자의 프로세스에서**특성을로 설정 하면 레지스트리에서 **Inproc** 서버 키가 추가 된 것을 알 수 있습니다 .이는 구성 요소 서비스 서로게이트 .dll을 가리킵니다.  
  
 구성 요소 서비스 (또는 Windows NT를 사용 하는 경우 Microsoft Transaction Service)에 대 한 자세한 내용 및 이러한 단계를 수행 하는 방법에 대 한 자세한 내용은 Microsoft Transaction Server 웹 사이트를 참조 하십시오.


