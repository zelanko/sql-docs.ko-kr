---
title: Microsoft ActiveX Data Objects (ADO) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 05cc5d08785b116f4e4dd27b8a0a61b34a14d473
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699392"
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ADO(ActiveX Data Objects)

ADO는 C++ SQL Server에 연결 하는 프로그램입니다. 물론, 또한 작동 클라우드에서 Azure SQL Database에 연결 합니다.

이 문서의 각 섹션에는 ADO의 구성 요소를 설명합니다.

> [!NOTE]
> ADO.NET ADO와 다릅니다. ADO.NET 및 다른 많은 SQL 연결 드라이버 및 해당 언어에 대해서는 설명부터 [SQL Server 드라이버](../connect/sql-connection-libraries.md)합니다.

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX Data Objects (ADO) 다양 한 OLE DB 공급자를 통해 원본에서에서 데이터 액세스 및 조작 하도록 클라이언트 응용 프로그램을 사용 하도록 설정 합니다. 기본 이점은 해당 사용 하기 쉽고, 높은 속도, 메모리 오버 헤드를 작은 디스크 공간을 보여 줍니다. ADO는 클라이언트/서버 및 웹 기반 응용 프로그램을 구축 하기 위한 주요 기능을 지원 합니다.  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX Data Objects (다차원) (ADO MD) Microsoft Visual Basic 및 Microsoft Visual과 같은 언어의 다차원 데이터에 쉽게 액세스를 제공 C++입니다. ADO MD Microsoft ActiveX 데이터 개체 (ADO) CubeDef 및 셀 집합 개체와 같은 다차원 데이터에 특정 개체를 포함 하도록 확장 합니다. ADO MD를 사용 하 여 다차원 스키마 찾아보기는 큐브를 쿼리 및 결과 검색할 수 있습니다.  
  
 ADO, 마찬가지로 ADO MD 데이터에 액세스 하는 기본 OLE DB 공급자를 사용 합니다. ADO MD를 사용 하려면 OLE DB OLAP 사양에 정의 된 대로 공급자는 다차원 데이터 (MDP 공급자) 여야 합니다. 와 달리 테이블 형식 데이터 공급자 (Tdp) 다차원 뷰에서 데이터 있는 데이터 테이블 형식 뷰에 제공합니다. 공급자에서 지원 되는 동작과 특정 구문에 대 한 자세한 정보에 대 한 OLAP OLE DB 공급자에 대 한 설명서를 참조 하십시오.  
  
## <a name="rds"></a>RDS  
 원격 데이터 서비스 (RDS)에 있는 클라이언트 응용 프로그램 또는 웹 페이지에는 서버에서 데이터를 이동, 클라이언트에서 데이터를 조작 하 수 단일 왕복에서 서버에 업데이트를 반환 하는 ADO의 기능입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="adox"></a>ADOX  
 데이터 정의 언어 및 보안 (ADOX)에 대 한 Microsoft ActiveX 데이터 개체 확장은 ADO 개체 및 프로그래밍 모델을 확장 합니다. ADOX는 스키마 만들기 및 수정 뿐만 아니라 보안 개체가 포함 됩니다. 스키마 조작 하는 개체 기반 접근 방식 이기 때문에 작동 하는 다양 한 데이터에 대 한 기본 구문의의 차이 관계 없이 소스 코드를 작성할 수 있습니다.  
  
 ADOX에 핵심 ADO 개체 도우미 라이브러리입니다. 만들기, 수정 및 삭제, 테이블 및 프로시저와 같은 스키마 개체에 대 한 추가 개체를 노출 합니다. 또한 사용자 및 그룹을 유지 하 고을 부여 하 고 개체에 대 한 권한을 취소 보안 개체가 포함 됩니다.  
  
## <a name="documentation"></a>설명서  
 [ADO 보안 디자인 문제](../ado/guide/ado-security-design-issues.md)  
  
 [ADO 프로그래머 가이드](../ado/guide/ado-programmer-s-guide.md)  
  
 ADO, RDS, ADO MD 및 ADOX를 사용 하 여 소개 합니다.  
  
 [ADO 프로그래머 참조](../ado/reference/ado-programmer-s-reference.md)  
  
 ADO 설명서의이 섹션에서는 각 ADO, RDS, ADO MD 및 ADOX 개체, 컬렉션, 속성, 동적 속성, 메서드, 이벤트 및 열거형에 대 한 항목을 포함합니다.  
  
 [ADO 용어 설명](../ado/ado-glossary.md)  
  
## <a name="support"></a>지원  
 ADO 문제 도움말 무료로 ADO 공개 뉴스 그룹에 게시를 시도 하세요. 이 뉴스 그룹에는 ADO를 포함 하는 Microsoft 기술 지원 서비스 (PSS) 기술 지원 전문가가 및 다른 숙련 된 ADO 개발자가 모니터링 됩니다.  
  
 지원 옵션에 대 한 자세한 내용은 Microsoft 도움말 및 지원 웹 사이트에서 찾을 수 있습니다.


