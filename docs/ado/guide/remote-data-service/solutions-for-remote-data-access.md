---
title: "원격 데이터 액세스를 위한 솔루션 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9030af4a02555aac77428ba9490ee72e87b93681
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="solutions-for-remote-data-access"></a>원격 데이터 액세스를 위한 솔루션
## <a name="the-issue"></a>문제  
 ADO 응용을 프로그램을 직접 액세스 하 고 (2 계층 시스템) 데이터 원본을 수정할 수 있습니다. 예를 들어 경우 연결이 데이터를 포함 하는 데이터 원본에 사용자가 직접 연결 2 계층 시스템.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 그러나 다음 데이터 원본에 액세스 직접 등 Microsoft® 인터넷 정보 서비스 (IIS) 매개 자를 통해 하는 것이 좋습니다. 이러한 작업에는 3 계층 시스템을 라고도 합니다. IIS는 인터넷 또는 인트라넷에서 원격 또는 서버에 프로그램을 호출 하는 로컬 또는 클라이언트 응용 프로그램에 대 한 효율적인 방법을 제공 하는 클라이언트/서버 시스템입니다. 서버 프로그램 데이터 원본에 액세스할 수 및 선택적으로 가져온된 데이터를 처리 합니다.  
  
 예를 들어 인트라넷 웹 페이지는 Microsoft® Visual Basic Scripting Edition (VBScript) IIS에 연결 하는 작성 된 응용 프로그램을 포함 합니다. IIS에 실제 데이터 원본에 연결 하며 데이터를 검색 하 어떤 식으로든에서 처리 한 다음 응용 프로그램에 처리 된 정보를 반환 합니다.  
  
 이 예제에서는 하지 응용 프로그램에 직접 연결 데이터 원본. IIS 않았습니다. 및 IIS ADO를 사용 하 여 데이터를 액세스 합니다.  
  
> [!NOTE]
>  인터넷 또는 인트라넷 기반으로 하지 않아도 클라이언트/서버 응용 프로그램 (즉, 웹 기반)-프로그램이 로컬 영역 네트워크에 구성 될 수 있습니다. 그러나 일반적인 경우는 웹 기반 응용 프로그램.  
  
 그리드, 확인란, 목록 등의 일부 시각적 컨트롤 반환 된 정보를 사용할 수 있습니다, 때문에 시각적 컨트롤에서 반환 된 정보를 쉽게 사용 되어야 합니다.  
  
 간단 하 고 효율적인 응용 프로그램 프로그래밍 인터페이스를 3 계층 시스템을 지원 하 고 정보를 반환 쉽게 검색 한 경우에 따라 2 계층 시스템에서 사용 하는 것이 좋습니다. 원격 데이터 서비스 (RDS)는이 인터페이스입니다.  
  
## <a name="the-solution"></a>솔루션  
 프로그래밍 모델을 정의 하는 RDS-일련의 액세스 하 고 데이터 소스를 업데이트 하는 데 필요한 활동-인터넷 정보 서비스 (IIS)와 같은 매개 자를 통해 데이터에 대 한 액세스 권한을 얻으려고 합니다. Rds.의 전체 기능을 요약 하는 프로그래밍 모델  
  
## <a name="see-also"></a>관련 항목:  
 [기본 RDS 프로그래밍 모델](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [RDS 시나리오](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 사용량 및 보안](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



