---
description: 원격 데이터 액세스에 대한 솔루션
title: 원격 데이터 액세스를 위한 솔루션 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
author: rothja
ms.author: jroth
ms.openlocfilehash: d337ef92600dbda0a54d2c2c51ab4e8caeed646c
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759213"
---
# <a name="solutions-for-remote-data-access"></a>원격 데이터 액세스에 대한 솔루션
## <a name="the-issue"></a>문제  
 ADO를 사용 하면 응용 프로그램에서 데이터 원본에 직접 액세스 하 고 수정할 수 있습니다 (때로는 2 계층 시스템 이라고 함). 예를 들어 데이터를 포함 하는 데이터 원본에 연결 하는 경우이는 2 계층 시스템에서 직접 연결 됩니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 그러나 Microsoft® 인터넷 정보 서비스 (IIS)와 같은 중개자를 통해 간접적으로 데이터 원본에 액세스할 수 있습니다. 이러한 정렬을 3 계층 시스템이 라고도 합니다. IIS는 로컬 또는 클라이언트 응용 프로그램에서 인터넷 또는 인트라넷을 통해 원격 또는 서버 프로그램을 호출 하는 효율적인 방법을 제공 하는 클라이언트/서버 시스템입니다. 서버 프로그램은 데이터 원본에 대 한 액세스 권한을 획득 하 고 필요에 따라 획득 한 데이터를 처리 합니다.  
  
 예를 들어 인트라넷 웹 페이지에는 IIS에 연결 되는 VBScript (Microsoft® Visual Basic Scripting Edition)로 작성 된 응용 프로그램이 포함 됩니다. 그러면 IIS가 실제 데이터 원본에 연결 하 고, 데이터를 검색 하 고, 특정 방식으로 처리 한 다음, 처리 된 정보를 응용 프로그램에 반환 합니다.  
  
 이 예제에서 응용 프로그램은 데이터 원본에 직접 연결 되지 않습니다. IIS가 수행 되었습니다. 및 IIS는 ADO를 통해 데이터에 액세스 했습니다.  
  
> [!NOTE]
>  클라이언트/서버 응용 프로그램은 인터넷 이나 인트라넷 (웹 기반)을 기반으로 할 필요가 없으며, 로컬 영역 네트워크에는 컴파일된 프로그램 으로만 구성 될 수 있습니다. 그러나 일반적인 경우는 웹 기반 응용 프로그램입니다.  
  
 그리드, 확인란 또는 목록과 같은 일부 시각적 컨트롤은 반환 된 정보를 사용할 수 있으므로 반환 된 정보를 시각적 컨트롤에서 쉽게 사용할 수 있어야 합니다.  
  
 3 계층 시스템을 지 원하는 간단 하 고 효율적인 응용 프로그램 프로그래밍 인터페이스를 원합니다. 이러한 인터페이스는 2 계층 시스템에서 검색 된 것 처럼 쉽게 정보를 반환 합니다. RDS (원격 데이터 서비스)가이 인터페이스입니다.  
  
## <a name="the-solution"></a>솔루션  
 RDS는 프로그래밍 모델을 정의 합니다. 데이터 원본에 액세스 하 고 업데이트 하는 데 필요한 일련의 작업을 사용 하 여 인터넷 정보 서비스 (IIS)와 같은 중개자를 통해 데이터에 액세스할 수 있습니다. 프로그래밍 모델에는 RDS의 전체 기능이 요약 되어 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [기본 RDS 프로그래밍 모델](./basic-rds-programming-model.md)   
 [RDS 시나리오](./rds-scenario.md)   
 [RDS 자습서](./rds-tutorial.md)   
 [RDS 사용량 및 보안](./rds-usage-and-security.md)