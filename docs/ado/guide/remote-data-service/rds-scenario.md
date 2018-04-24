---
title: RDS 시나리오 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8260049ad0bd4022cfd9ff3382d04cbb16c5dfac
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="rds-scenario"></a>RDS 시나리오
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 주소록 응용 프로그램은 데이터 서비스 RDS (원격)를 사용 하 여 간단 하 고 데이터 인식 웹 응용 프로그램을 작성 하는 방법을 보여 주는 시나리오-온라인 회사 주소록 합니다. 이 시나리오는 Microsoft Visual Basic Scripting Edition (VBScript)에 대 한 유용 및 COM 프로그래머에 게를 RDS를 사용 데이터 인식 ActiveX 컨트롤을 사용 하는 방법을 알아보고 하려는 개발자 경험이 많은 소프트웨어에 대 한 데이터 중심 웹 응용 프로그램을 빌드 인 합니다.  
  
 이 시나리오에서는 ActiveX 컨트롤 기본 HTML 레이아웃 태그, 사용 하 여 DHTML 데이터 바인딩 기술 및 프로그램을 사용 하는 방법을 알고 있다고 가정 합니다.  
  
 SDK를 설치한 경우 주소록 예제 응용 프로그램에 대 한 전체 소스 코드에서 samples\dataaccess\rds\AddressBook\AddressBook.asp SDK 디렉터리에 있습니다. 주소록 시나리오를 보려면 Internet Explorer 4.0 이상 버전에서는 입력 **http://*웹 서버*/RDS/AddressBook/AddressBook.asp** 여기서 *웹 서버* 지정 되는 이름 Windows NT 4.0 또는 Windows 2000 웹 서버 컴퓨터에 인터넷 정보 서비스 (IIS) 및 ASP 실행 되는.  
  
## <a name="introduction-to-address-book"></a>주소록 소개  
 주소록 샘플 응용 프로그램에는 간단한 온라인 주소록 인트라넷을 통해 검색 가능한 디렉터리를 게시 하는 데 사용할 수 있는 제공 합니다. 주소록은 사용자 직원에 대 한 정보를 요청 하는 하나 이상의 필드에 검색 문자열을 입력할 수 있도록 설계 되었습니다. 원격 데이터 서비스의 기본 기능을 표시 하려면 예제 응용 프로그램 개체 및 검색 필드의 최소 수도 작은 보관 의도적으로 됩니다.  
  
 응용 프로그램 인터페이스는 다음과 같은 부분으로 구성 됩니다.  
  
-   보이지 않는 **.rds입니다 DataControl** 클라이언트에서 데이터베이스에 연결 하는 데 사용 되는 데이터 바인딩 개체입니다.  
  
-   직원 특성에 대 한 입력 필드로 작동 하는 HTML 텍스트 상자에 검색 조건을 합니다.  
  
-   검색 필드의 선택을 취소 하 데이터베이스에서 직원 정보 업데이트 보류 중인 변경 내용, 취소를 표에 표시 된 데이터의 행을 이동 하는 쿼리를 작성 하기 위해 HTML 명령 단추 합니다.  
  
-   백 엔드 데이터베이스에 대해 쿼리에서 반환 된 데이터를 표시할 DHTML 데이터 바인딩 (통해는 **.rds입니다 DataControl** 데이터 바인딩 개체)는 테이블에 있습니다.  
  
-   각각의 앞서 언급 한 요소를 연결 하 고 상호 작용 하도록 허용 하는 VBScript 루틴입니다. VBScript 코드는 또한 초기화는 **.rds입니다 DataControl** 개체를 동적으로의 이름에서 HTML 테이블에 열 머리글을 만드는 **.rds입니다 DataControl** 레코드 집합 필드.  
  
 단계의 단계를 설정 하 고 시나리오를 실행 하 고 시나리오의 작동 방식에 대 한 자세한 내용을 보려면 링크를 클릭 합니다.  
  
 이 시나리오는 다음 항목을 포함합니다.  
  
-   [주소록 응용 프로그램에 대한 시스템 요구 사항](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [주소록 SQL 스크립트 실행](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [주소록 예제 응용 프로그램 실행](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [주소록 데이터 바인딩 개체](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [주소록 명령 단추](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [주소록 탐색 단추](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>관련 항목:  
 [주소록 응용 프로그램에 대 한 시스템 요구 사항](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)


