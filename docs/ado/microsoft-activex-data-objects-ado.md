---
title: Microsoft ADO(ActiveX Data Objects) (ADO) | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18b9a6590ce777402456c8e9f8c8f28807ec5670
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606615"
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ADO(ActiveX Data Objects)

ADO(ActiveX Data Objects)은 지정 된 백 엔드 엔진에 종속 되지 않음을 의미 하는 프로그래밍 모델입니다. 그러나 현재 ADO 모델을 지 원하는 유일한 엔진은 OLE DB입니다. ODBC 용 OLE DB 공급자는 물론 많은 네이티브 OLE DB 공급자가 있습니다. ADO는 c + + 및 Visual Basic 프로그램에서 SQL Server 및 기타 데이터베이스에 연결 하는 데 사용 됩니다. 물론 클라우드의 Azure SQL Database에 연결 하는 것도 마찬가지입니다.

이 문서의 각 섹션에서는 ADO의 구성 요소에 대해 설명 합니다.

> [!NOTE]
> ADO.NET는 ADO와 다릅니다. ADO.NET 및 기타 많은 SQL 연결 드라이버와 해당 언어에 대해서는 [SQL Server 드라이버](../connect/sql-connection-libraries.md)부터 설명 합니다.

  
## <a name="ado"></a>ADO  
 ADO (Microsoft ADO(ActiveX Data Objects))를 사용 하면 클라이언트 응용 프로그램이 OLE DB 공급자를 통해 다양 한 원본에서 데이터에 액세스 하 고 조작할 수 있습니다. 기본 이점은 사용 편의성, 고속, 낮은 메모리 오버 헤드 및 작은 디스크 공간입니다. ADO는 클라이언트/서버 및 웹 기반 응용 프로그램을 빌드하기 위한 주요 기능을 지원 합니다.  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX Data Objects(다차원) (ADO MD)를 사용 하면 Microsoft Visual Basic 및 Microsoft Visual C++ 같은 언어의 다차원 데이터에 쉽게 액세스할 수 있습니다. ADO MD는 CubeDef 및 Cellset 개체와 같은 다차원 데이터에 특정 한 개체를 포함 하도록 ADO (Microsoft ADO(ActiveX Data Objects))를 확장 합니다. ADO MD 다차원 스키마를 찾아보고, 큐브를 쿼리하고, 결과를 검색할 수 있습니다.  
  
 ADO와 마찬가지로 ADO MD 기본 OLE DB 공급자를 사용 하 여 데이터에 대 한 액세스 권한을 얻습니다. ADO MD를 사용 하려면 공급자가 OLAP 사양 OLE DB에 정의 된 대로 .MDP (multidimensional data provider) 여야 합니다. MDPs는 테이블 형식 보기에서 데이터를 제공 하는 TDPs (tabular data provider)와는 달리 다차원 뷰에서 데이터를 제공 합니다. 공급자가 지 원하는 특정 구문 및 동작에 대 한 자세한 내용은 OLAP OLE DB 공급자에 대 한 설명서를 참조 하세요.  
  
## <a name="rds"></a>RDS  
 RDS (원격 데이터 서비스)는 ADO의 기능으로, 서버에서 클라이언트 응용 프로그램이 나 웹 페이지로 데이터를 이동 하 고, 클라이언트에서 데이터를 조작 하 고, 단일 왕복으로 서버에 업데이트를 반환할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="adox"></a>ADOX  
 ADOX (데이터 정의 언어 및 보안)에 대 한 Microsoft ADO(ActiveX Data Objects) 확장은 ADO 개체 및 프로그래밍 모델에 대 한 확장입니다. ADOX에는 스키마를 만들고 수정할 뿐만 아니라 보안을 위한 개체가 포함 되어 있습니다. 스키마 조작을 위한 개체 기반 방법 이므로 네이티브 구문의 차이점에 관계 없이 다양 한 데이터 원본에 대해 작동 하는 코드를 작성할 수 있습니다.  
  
 ADOX는 핵심 ADO 개체에 대 한 도우미 라이브러리입니다. 테이블, 프로시저 등의 스키마 개체를 만들고 수정 하 고 삭제 하기 위한 추가 개체를 제공 합니다. 또한 사용자 및 그룹을 유지 관리 하 고 개체에 대 한 사용 권한을 부여 하 고 취소 하는 보안 개체를 포함 합니다.  
  
## <a name="documentation"></a>설명서  
 [ADO 보안 디자인 문제](../ado/guide/ado-security-design-issues.md)  
  
 [ADO 프로그래머 가이드](../ado/guide/ado-programmer-s-guide.md)  
  
 ADO, RDS, ADO MD 및 ADOX를 사용 하는 방법을 소개 합니다.  
  
 [ADO 프로그래머 참조](../ado/reference/ado-programmer-s-reference.md)  
  
 ADO 설명서의이 섹션에는 각 ADO, RDS, ADO MD 및 ADOX 개체, 컬렉션, 속성, 동적 속성, 메서드, 이벤트 및 열거형에 대 한 항목이 포함 되어 있습니다.  
  
 [ADO 용어 설명](../ado/ado-glossary.md)  
  
## <a name="support"></a>Support(지원)  
 ADO 문제에 대 한 무료 도움말을 보려면 ADO 공용 뉴스 그룹에 게시 해 보세요. 이 뉴스 그룹은 ADO를 다루는 Microsoft PSS (기술 지원 서비스) 지원 전문가와 기타 숙련 된 ADO 개발자에 의해 모니터링 됩니다.  
  
 지원 옵션에 대 한 자세한 내용은 Microsoft 도움말 및 지원 웹 사이트에서 찾을 수 있습니다.


