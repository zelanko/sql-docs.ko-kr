---
title: Microsoft ActiveX Data Objects (ADO) | Microsoft Docs
ms.custom: 
ms.date: 07/25/2017
ms.reviewer: 
ms.suite: 
ms.prod: sql-non-specified
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 28fa2c279cfd7964d8516514a3caed129e335692
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX Data Objects (ADO)

ADO는 c + + 프로그램에서 SQL Server에 연결 하는 데 사용 됩니다. 물론,도 작동 클라우드에서 Azure SQL 데이터베이스에 연결 합니다.

이 문서의 각 섹션 ADO의 구성 요소를 설명합니다.

> [!NOTE]
> ADO.NET은 ADO 다릅니다. ADO.NET 및 다른 많은 SQL 연결 드라이버 및 해당 언어에서 시작 설명 되어 [SQL Server 드라이버](../connect/sql-connection-libraries.md)합니다.

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX 데이터 개체 (ADO) 액세스 하 고 다양 한 OLE DB 공급자를 통해 원본에서에서 데이터를 조작 하면 클라이언트 응용 프로그램을 사용 하도록 설정 합니다. 기본 이점은 손쉬운 사용, 고속, 낮은 메모리 오버 헤드 및 디스크 공간을 조금 있습니다. ADO는 클라이언트/서버 및 웹 기반 응용 프로그램을 구축 하기 위한 주요 기능을 지원 합니다.  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX Data Objects (다차원) ADO MD ()과 같은 Microsoft Visual Basic 및 Visual c + + 언어의 다차원 데이터에 쉽게 액세스를 제공합니다. ADO MD Microsoft ActiveX 데이터 개체 (ADO) CubeDef 및 셀 집합 개체와 같은 다차원 데이터에 특정 개체를 포함 하도록 확장 합니다. ADO MD 다차원 스키마 찾아보기는 큐브를 쿼리 하 고 사용할 수는 결과 검색 합니다.  
  
 ADO, 같은 ADO MD 데이터에 액세스 하는 기본 OLE DB 공급자를 사용 합니다. ADO MD를 사용 하려면 OLE DB OLAP 사양에 정의 된 대로 공급자는 다차원 데이터 (MDP 공급자) 여야 합니다. 와 반대로 테이블 형식 데이터 공급자 (Tdp) 다차원 뷰에서 데이터에에서 있는 데이터 테이블 형식 뷰의 표시 합니다. 특정 구문 및 공급자가 지원 되는 동작에 대 한 자세한 내용을 보려면 OLAP OLE DB 공급자에 대 한 설명서를 참조 하십시오.  
  
## <a name="rds"></a>RDS  
 원격 데이터 서비스 (RDS)에 있는 클라이언트 응용 프로그램 또는 웹 페이지에는 서버에서 데이터를 이동할 클라이언트에서 데이터를 조작 하 고 사용할 수는 단일 왕복에서 서버에 업데이트를 반환 하는 ADO의 기능입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="adox"></a>ADOX  
 데이터 정의 언어 및 보안 (ADOX)에 대 한 Microsoft ActiveX 데이터 개체 확장은 ADO 개체 및 프로그래밍 모델에 대 한 확장입니다. ADOX 보안 뿐만 아니라 스키마 만들기 및 수정에 대 한 개체를 포함합니다. 스키마 조작 하는 개체 기반 방식 이기 때문에 기본 구문의의 차이 관계 없이 원본 다양 한 데이터에 대해 작동 하는 코드를 작성할 수 있습니다.  
  
 ADOX는 코어 ADO 개체를 도우미 라이브러리입니다. 만들기, 수정 및 삭제 테이블 및 프로시저와 같은 스키마 개체에 대 한 추가 개체를 노출 합니다. 또한 사용자 및 그룹을 유지 관리 권한을 부여 하 고 개체에 사용 권한을 취소 하려면 보안 개체를 포함 합니다.  
  
## <a name="documentation"></a>설명서  
 [ADO 보안 디자인 문제](../ado/guide/ado-security-design-issues.md)  
  
 [ADO 프로그래머 가이드](../ado/guide/ado-programmer-s-guide.md)  
  
 ADO, RDS, ADO MD ADOX를 사용 하 여 소개 합니다.  
  
 [ADO 프로그래머 참조](../ado/reference/ado-programmer-s-reference.md)  
  
 ADO 설명서의이 섹션에는 각 ADO, RDS, ADO MD 및 ADOX 개체, 컬렉션, 속성, 동적 속성, 메서드, 이벤트 및 열거형에 대 한 항목이 포함 되어 있습니다.  
  
 [ADO 용어 설명](../ado/ado-glossary.md)  
  
## <a name="support"></a>지원  
 ADO 문제에 대 한 도움말을 무료로 ADO 공용 뉴스 그룹에 게시를 시도 하세요. 이 뉴스 그룹은 Microsoft 기술 지원 서비스 (PSS) 지원 전문가 게 ADO를 포함 하 고 다른 숙련 된 ADO 개발자가 모니터링 됩니다.  
  
 지원 옵션에 대 한 자세한 내용은 Microsoft 도움말 및 지원 웹 사이트에서 찾을 수 있습니다.



