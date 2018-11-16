---
title: DCOM에서 실행 하도록 DLL 사용 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e45dff30c67f94abb58afcf19d151dd02d33c161
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559730"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>DCOM에서 실행하도록 DLL 사용
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 다음 단계에는 DCOM 및 Microsoft 인터넷 정보 서비스 (HTTP) 구성 요소 서비스를 통해 모두 사용 하 여 비즈니스 개체.dll을 사용 하도록 설정 하는 방법을 간략하게 설명 합니다.  
  
1.  구성 요소 서비스 MMC 스냅인에서 비어 있는 새 패키지를 만듭니다.  
  
     패키지를 만들고이 패키지에 DLL을 추가 하려면 구성 요소 서비스 MMC 스냅인을 사용 합니다. 따라서.dll DCOM을 통해 액세스할 수 있지만 IIS 통해 액세스 가능성을 제거 합니다. (.Dll을 레지스트리에서 확인 하는 경우는 **Inproc** 키가 비어 있는 이제;이 항목의 뒷부분에서 설명 하 고 활성화 특성을 설정에 값을 추가 합니다 **Inproc** 키입니다.)  
  
2.  패키지에 비즈니스 개체를 설치 합니다.  
  
     -또는-  
  
     가져오기의 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 패키지에는 개체입니다.  
  
3.  패키지에 대 한 활성화 특성을 설정 **작성자의 프로세스에서** (라이브러리 응용 프로그램).  
  
     .Dll에 동일한 컴퓨터에서 DCOM 및 IIS를 통해 액세스할 수 있도록 구성 요소 서비스 MMC 스냅인에서 구성 요소의 활성화 특성을 설정 해야 합니다. 특성 설정한 후 **작성자의 프로세스**는 **Inproc** 구성 요소 서비스를 가리키는 대리.dll을 레지스트리에 서버 키가 추가 되었습니다.  
  
 구성 요소 서비스 (또는 Microsoft Transaction 서비스, Windows NT를 사용 하는 경우)에 대 한 자세한 방법과 이러한 단계를 수행 하려면 Microsoft Transaction Server 웹 사이트를 방문 합니다.


