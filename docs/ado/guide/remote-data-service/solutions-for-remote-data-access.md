---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 302a43238c755890e9fd106d8784eabdd0361d88
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558620"
---
# <a name="solutions-for-remote-data-access"></a>원격 데이터 액세스에 대한 솔루션
## <a name="the-issue"></a>문제  
 ADO 응용을 프로그램을 직접 액세스 하 고 (2 계층 시스템) 데이터 원본을 수정할 수 있습니다. 예를 들어 데이터가 포함 된 데이터 원본에 대 한 연결 인 경우는 직접 연결 2 계층 시스템에서.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 그러나 다음 하지 데이터 원본에 직접 액세스할 수와 같은 Microsoft® 인터넷 정보 서비스 (IIS) 매개 자를 통해는 것이 좋습니다. 이 배열에는 3 계층 시스템을 라고 합니다. IIS는 인터넷 또는 인트라넷에서 원격 또는 서버에서 프로그램을 호출 하는 로컬 또는 클라이언트 응용 프로그램에 대 한 효율적인 방법을 제공 하는 클라이언트/서버 시스템입니다. 서버 프로그램 데이터 원본에 대 한 액세스를 얻게 하 고 필요에 따라 받은 데이터를 처리 합니다.  
  
 예를 들어 인트라넷 웹 페이지는 Microsoft® Visual Basic Scripting Edition (VBScript)를 IIS에 연결 하는 작성 된 응용 프로그램을 포함 합니다. IIS에 실제 데이터 원본에 연결 하며 데이터를 검색 하 어떤 식으로든에서 처리를 응용 프로그램에 처리 정보를 반환 합니다.  
  
 이 예제에서는 되지 응용 프로그램에 직접 연결 데이터 소스 IIS 않았습니다. 및 IIS ADO를 사용 하 여 데이터에 액세스 합니다.  
  
> [!NOTE]
>  클라이언트/서버 응용 프로그램이 인터넷 또는 인트라넷 기반으로 할 필요가 없습니다 (즉, 웹 기반)-로컬 영역 네트워크에서 컴파일된 프로그램으로 구성 될 수 있습니다. 그러나 일반적인 경우는 웹 기반 응용 프로그램.  
  
 표나 확인란, 목록 등의 몇 가지 시각적 컨트롤에 반환 된 정보를 사용할 수 있으므로 시각적 컨트롤에서 반환 된 정보를 쉽게 사용 되어야 합니다.  
  
 3 계층 시스템을 지 원하는 반환 하는 정보를 쉽게 검색 한 것 처럼 2 계층 시스템에서 응용 프로그램 프로그래밍 인터페이스를 간단 하 고 효율적으로 해야 합니다. 원격 데이터 서비스 (RDS)는이 인터페이스입니다.  
  
## <a name="the-solution"></a>솔루션  
 RDS 프로그래밍 모델을 정의-일련의 활동에 액세스할 수 있고 데이터 원본을 업데이트 하는 데 필요한-인터넷 정보 서비스 (IIS)와 같은 매개 자를 통해 데이터에 액세스할 수 있습니다. Rds.의 전체 기능을 요약 하는 프로그래밍 모델  
  
## <a name="see-also"></a>관련 항목  
 [기본 RDS 프로그래밍 모델](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [RDS 시나리오](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 사용량 및 보안](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


