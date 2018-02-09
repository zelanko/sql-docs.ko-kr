---
title: "DCOM 실행 되도록 DLL을 사용 하도록 설정 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 65401d1e0f3da015982d27aa7608cba4046313a2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>DCOM에서 실행 하는 DLL을 사용 하도록 설정
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 다음 단계에는 비즈니스 개체.dll DCOM 및 Microsoft 인터넷 정보 서비스 (HTTP)를 통해 구성 요소 서비스를 모두 사용할 수 있게 하는 방법을 간략하게 설명 합니다.  
  
1.  구성 요소 서비스 MMC 스냅인에서 비어 있는 새 패키지를 만듭니다.  
  
     패키지를 만들고이 패키지에는 DLL을 추가 하는 구성 요소 서비스 MMC 스냅인을 사용 합니다. 이렇게 하면.dll DCOM을 통해 액세스할 수 있지만 IIS 통해 액세스 가능성을 제거 합니다. (.Dll에 대 한 레지스트리를 확인 하는 경우는 **Inproc** 키 비어 이제는이 항목의 뒷부분에 설명 된 정품 인증 특성을 설정에 값 추가 **Inproc** 키입니다.)  
  
2.  패키지에 비즈니스 개체를 설치 합니다.  
  
     -또는-  
  
     가져오기는 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 패키지에는 개체입니다.  
  
3.  패키지에 대 한 활성화 특성을 설정 **작성자의 프로세스에서** (라이브러리 응용 프로그램).  
  
     .Dll을 동일한 컴퓨터에서 DCOM 및 IIS를 통해 액세스할 수 있도록 구성 요소 서비스 MMC 스냅인에서 구성 요소의 활성화 특성을 설정 해야 합니다. 특성을 설정 후 **작성자의 프로세스에서**, 것을 확인할 수는 **Inproc** 대리.dll을 가리키도록 구성 요소 서비스는 레지스트리의 서버 키가 추가 되었습니다.  
  
 구성 요소 서비스 (또는 Microsoft Transaction 서비스, Windows NT를 사용 하는 경우)에 대 한 자세한 내용은 Microsoft Transaction Server 웹 사이트를 방문 하십시오 이러한 단계를 수행 하는 방법과 합니다.


